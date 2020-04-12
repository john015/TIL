## Webpack이란?

`Webpack`은 모던 Javascript Application을 위한 Static Module Bundler입니다.

Webpack이 Application를 처리할 때, 내부적으로는 프로젝트에서 필요한 모든 모듈들을 매핑하고 1개 이상의 번들을 생성하는 [Dependencies Graph](https://webpack.js.org/concepts/dependency-graph/)를 만듭니다.

## Entry

`entry` 프로퍼티는 `webpack` 내부에 위치한 `dependency graph`의 시작점을 지정하기 위해 사용합니다.

`webpack`은 `entry` 지점으로부터 직간접적으로 의존적인 모듈 및 라이브러리를 모두 찾아서 `Dependencies Graph`에 추가합니다.

`entry`의 기본값은 `./src/index.js`이며, `webpack.config.js`에 `entry` 프로퍼티를 추가해서 다른 여러 시작점을 지정할 수 있습니다.

```javascript
// webpack.config.js
module.exports = {
  // ./src/entry/file.js 파일을 dependency graph의 시작점으로 지정
  entry: './src/entry/file.js'
};
```

## Output

`output` 프로퍼티는 생성한 번들을 내보낼 경로나 내보낼 번들의 파일명을 지정하기 위해 사용합니다.

해당 프로퍼티를 지정하지 않을경우 기본적으로 main file의 경우 `./dist/main.js` 경로에 생성되며, 다른 파일들은 `./dist` 폴더안에 생성됩니다.

```javascript
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/entry/file.js'
  output: {
    // ./dist 경로에 파일 생셩
    path: path.resolve(__dirname, 'dist'),
    // 내보낼 파일명을 bundle.js로 지정
    filename: 'bundle.js'
  }
};
```

## Loaders

`webpack`은 오직 `JavaScript`와 `JSON` 파일만 이해할 수 있습니다. 그래서 다른 타입(ts, css, etc..)의 파일들을 처리할려면 `loader`를 사용해야합니다.

`loader`는 `webpack`이 기본적으로 처리할 수 없는 타입의 파일들을 처리하여 내 애플리케이션에서 사용할 수 있고, `dependency graph`에 추가할 수 있는 유효한 형태의 모듈로 변환할 수 있도록 도와줍니다.

high level에서, `loaders`는 두 가지 프로퍼티를 가지고 있습니다.

- `test` 프로퍼티는 어느 파일이 변환(transform)되어야 하는지를 나타냅니다.
- `use` 프로퍼티는 해당 파일을 변환하기 위해서 어떤 `loader`를 사용해야하는지 나타냅니다.

`use` 프로퍼티의 값으로 배열을 넘겨줄 수 있는데, 배열을 넘겨줄 경우 배열의 로더들을 뒤에서 부터 순차적으로 적용시킵니다. 

`Loaders`는 Node.js 런타임에서 동작하며 Node.js 환경에서 사용 가능한 모든 것을 할 수 있습니다.

```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      // css-loader를 먼저 적용한 뒤 style-loader 적용
      { test: /\.css$/, use: ['style-loader', 'css-loader'] }
    ]
  }
};
```

위 코드를 `webpack.config.js`에 추가하면 `webpack` 컴파일러는 `import`, `require` 구문안에 `.css` 확장자 파일 경로가 선언되어 있으면 `css-loader`를 사용하여 해당 파일을 처리한뒤, 번들에 추가합니다.

> `webpack.config.js` 파일에 `rules`를 정의할 때 `rules` 프로퍼티가 아닌 `module.rules`로 정의해야 합니다. 만약 잘못 설정 되었을 경우 `webpack`은 사용자에게 경고해줍니다.

## Plugins

`loaders` 는 특정 타입의 모듈을 변환하기 위해 사용되지만, `plugins`은 번들 최적화, asset 관리, 환경 변수 주입과 같은 번들된 결과물에 대하여 광범위한 작업을 수행하기 위해 사용합니다.

`plugin`을 사용하기 위해선, commonJs 방식(`require()`)으로 플러그인을 가져온 뒤 해당 플러그인을 `plugins` 배열에 추가하면 됩니다. 

대부분의 플러그인들은 옵션을 통해서 커스터마이징을 할 수 있습니다. 

플러그인은 다양한 목적에 의해 여러번 사용될 수 있으므로, 플러그인을 호출 할 때 `new` 연산자와 함께 호출해서 인스턴스 형태로 만들어줘야합니다.

```javascript
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin'); // npm/yarn을 통해 설치된 html-webpack-plugin 플러그인을 불러옴
const webpack = require('webpack'); // webpack built-in 플러그인에 접근하기 위해 사용 

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```

`webpack.config.js` 파일안에서 플러그인을 사용하는 것은 간단하지만 탐구할 가치가 있는 많은 use case들이 있기 때문에 [Plugins docs](https://webpack.js.org/concepts/plugins/) 를 참고

## Mode

`mode` 옵션을 설정하면 웹팩은 해당 mode에 맞는 built-in 최적화를 알아서 해줍니다. 

`mode` 는 `development`, `production`, `none` 으로 지정할 수 있으며, 기본값은 `production` 입니다.

`mode` 옵션을 사용하기 위해선, `webpack.config.js`에 `mode` 프로퍼티를 설정 해주거나, webpack을 실행할 때 cli상에서 `--mode` argument를 전달해주면 됩니다.

```javascript
// webpack.config.js
module.exports = {
  mode: 'development'
};
```

or 

```sh
webpack --mode=development
```

| Option        | Description |
|---------------|-------------|
| `development` | `DefinePlugin` 플러그인의 `process.env.NODE_ENV`값을 `development` 로 설정. `NamedChunksPlugin`, `NamedModulesPlugin` 플러그인 활성화 |
| `production`  | `DefinePlugin` 플러그인의 `process.env.NODE_ENV`값을 `production` 로 설정. `FlagDependencyUsagePlugin` , `FlagIncludedChunksPlugin` , `ModuleConcatenationPlugin` , `NoEmitOnErrorsPlugin` , `OccurrenceOrderPlugin` , `SideEffectsFlagPlugin`, `TerserPlugin` 플러그인 활성화             |
| `none`        | 기본 최적화 옵션들을 적용 안하게 설정 |

> Note. `NODE_ENV`를 설정해도 `mode`가 자동으로 설정되지 않습니다.

각 모드를 설정할 경우, 웹팩이 정확히 어떤 옵션들을 켜주는지 궁금하면 [링크](https://webpack.js.org/configuration/mode/#mode-development)를 참고해주세요.

## Reference

- https://webpack.js.org/concepts/
- https://webpack.js.org/configuration/mode/