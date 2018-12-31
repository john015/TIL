## eslint 와 prettier 연동및 eslint airbnb sytle setting

**콘솔**

```
// eslint 와 prettier 연동
yarn add --dev prettier-eslint
// eslint airbnb 스타일
yarn add eslint-config-airbnb

```

**.eslintrc**

```
{
"parser": "babel-eslint",
"extends": "airbnb",
"plugins": ["react", "jsx-a11y", "import"],
"rules": {
"react/jsx-filename-extension": 0
}
}
```

## react 16.3 이후 라이프 싸이클

**componentDidMount**

- 컴포넌트가 화면에 나타나게 됐을 때 호출

**static getDerivedStateFromProps(nextProps, prevState)**

- props 로 받아온 값을 state 로 동기화 하는 작업을 해줘야 하는 경우에 사용

**shouldComponentUpdate(nextProps, nextState)**

- 기본적으로 true 를 반환 false 반환시 렌더링 x

**getSnapshotBeforeUpdate(prevProps, prevState)**

- DOM 변화가 일어나기 직전의 DOM 상태를 가져옴 리턴 값은 componentDidUpdate 에서 3 번째 아규먼트로 감

**componentDidUpdate(prevProps, prevState, snapshot)**

- DOM 변화가 발생한 뒤 발생 이 시점에선 this.props 와 this.state 가 바뀌어있음

**componentWillUnmount()**

- 언마운트 시 호출

**componentDidCatch(error, info)**

- 에러 발생시 호출

## jest package.json setting

```json
  // ts-jest install
  "jest": {
    "setupTestFrameworkScriptFile": "<rootDir>/src/setupTests.ts",
    "snapshotSerializers": [
      "enzyme-to-json/serializer"
    ],
    "transform": {
      ".(ts|tsx)": "<rootDir>/node_modules/ts-jest/preprocessor.js"
    },
    "moduleFileExtensions": [
      "ts",
      "tsx",
      "js"
    ],
    "globals": {
      "ts-jest": {
        "tsConfigFile": "./tsconfig.test.json"
      }
    },
    "collectCoverage": true,
    "testMatch": [
      "<rootDir>/src/**/__tests__/**/*.{js,jsx,tsx,ts}",
      "<rootDir>/src/**/?(*.)(spec|test).{js,jsx,tsx,ts}"
    ]
  }
```
