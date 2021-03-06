## Simentic Versioning(유의적 버전)

NPM은 퍼블리시된 패키지가 Simentic Versioning을 준수한다는 기준으로 해당 패키지 버전을 관리합니다.

Simentic Versioning은 주(Major), 부(Minor), 수(Patch) 세 가지 숫자를 조합해서 버전을 관리합니다. 어떤 패키지의 버전이 v16.13.0이라고 가정하면 Major 버전이 16, Minor 버전이 13, Patch 버전이 0입니다.

각 버전을 변경하는 기준은 다음과 같습니다.

- Major Version: 기존 버전과 호환되지 않게 변경한 경우
- Minor version: 기존 버전과 호환되면서 기능이 추가된 경우
- Patch version: 기존 버전과 호환되면서 버그를 수정한 경우

## 패키지 버전 관리

`package.json` 파일에서 버전을 관리할 때 그냥 버전을 적는 대신 캐럿(^)이나 틸드(~)를 prefix해서 버저닝을 할 수 있습니다,

물론 위 3개 방식 말고도 >, >=, <, <=같은 부등호로도 버저닝을 할 수 있습니다.

### 틸드(~)

틸드(~)는 마이너 버전이 명시되어 있으면 패치 버전을 업그레이드 하고, 마이너 버전이 명시 안 되어 있으면 캐럿(^)과 비슷하게 마이너 버전과 패치 버전을 업그레이드 합니다.

- `~0.1.2` : `>= 0.1.2, < 0.2.0`
- `~0` : `>= 0.0.0, < 1.0.0`

### 캐럿(^)

캐럿(^)은 마이너 버전과 패치 버전을 업그레이드 합니다.

패키지 버전이 1.0.0 미만인 경우(pre-release)에는 틸드(~)와 비슷하게 동작하며 버전이 0.0.x인 경우에는 하위 호환성 유지가 안 될 가능성이 높으므로 지정한 버전만을 사용합니다.

기본적으로 npm 패키지를 설치할 때 캐럿이 앞에 붙어서 package.json에 버저닝 됩니다.

- `^1.3` : `>= 1.3.0, < 2.0.0`
- `^0.1.2` : `>= 0.1.2, < 0.2.0`
- `^0.0.1` : `=== 0.0.1`
- `^0` : `>= 0.0.0, < 1.0.0`

## package-lock.json, yarn.lock이 필요한 이유

`package.json`에 정의된 패키지 버전이 absolute로 선언되어 있으면 문제없지만, 위처럼 틸드(~)나 캐럿(^)을 사용해서 선언되어 있으면, 설치 시점에 따라 버전이 달라질 수 있어서 예기치 못한 오류가 발생할 수 있습니다.

그래서 패키지 매니저로 `npm`을 사용하면 `package-lock.json`파일에, `yarn`을 사용하면 `yarn.lock`파일에 해당 패키지 최초 설치 당시 버전을 명시해줍니다.

그이후 `npm i`나 `yarn` 커맨드를 사용해서 패키지를 설치하면 캐럿이나 틸드를 사용했어도, 해당 lock파일에 명시된 버전으로 설치합니다.

## dependencies, devDependencies, peerDependencies 차이

### dependencies

`dependencies`는 `production` 환경에서 작동되어야 하는 패키지들입니다.(lodash, react, vue, angular, etc...)

`npm install (package name)` 커맨드로 패키지를 설치하면 `dependencies`에 추가됩니다.

### devDependencies

`devDependencies`는 `development` 환경에서만 작동되는 패키지들입니다.(webpack, babel, typescript, etc..)

`npm install -D (package name)` 커맨드로 패키지를 설치하면 `devDependencies`에 추가됩니다.

`devDependencies`에 해당하는 패키지들은 프로덕션 환경에서는 설치되지 않습니다.

### peerDependencies

내 패키지가 특정 다른 패키지와 함께 사용되도록 개발된 경우 해당 다른 패키지의 버저닝을 사용하는 쪽에서 지정하도록 하고싶을 때 피어 디펜더시에 추가할 수 있습니다.(ex. react에 의존하는 라이브러리일 경우 react를 peerDependencies에 추가)

`peerDependencies`에 해당하는 패키지들은 `npm install (my package naem)`시 `node_modules` 디렉토리에 설치되지 않고 해당 패키지가 사용 하는 쪽의 디펜던시에 없을 때만 에러를 cli상에 표시해줍니다.(npm v3 이전 버전에서는 디펜던시와 같이 설치됩니다)
