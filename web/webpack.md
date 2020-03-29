## Webpack이란?

`Webpack`은 모던 Javascript Application을 위한 Static Module Bundler입니다.

Webpack이 Application를 처리할 때, 내부적으로는 프로젝트에서 필요한 모든 모듈들을 매핑하고 1개 이상의 번들을 생성하는 [Dependencies Graph](https://webpack.js.org/concepts/dependency-graph/)를 만듭니다.

## entry

`entry`는 `webpack` 내부에 위치한 `dependency graph`의 시작점 모듈입니다.

`webpack`은 `entry` 지점으로부터 직간접적으로 의존적인 모듈 및 라이브러리를 모두 찾아서 `Dependencies Graph`에 추가합니다.

`entry`의 기본값은 `./src/index.js`이며, `webpack.config.js`에 `entry` 프로퍼티를 추가해서 다른 여러 시작점을 지정할 수 있습니다.

```javascript
// webpack.config.js
module.exports = {
  // ./src/entry/file.js 파일을 dependency graph의 시작점으로 지정
  entry: './src/entry/file.js'
};
```