# Tabnabbing

## Tabnabbing 공격이란?

- Tabnabbing이란 웹 페이지에서 링크(`target="_blank"`인 a 태그)를 클릭 했을 때, 새롭게 열린 탭 또는 창에서 링크가 포함되어있던 기존 문서의 location을 피싱 사이트로 변경해 정보를 탈취하는 피싱 기술을 뜻합니다.

## Tabnabbing 공격 절차

1. 사용자가 https://example.com에 접속합니다.
2. 사용자가 해당 웹 페이지에서 https://tabnabbing.example.com로 이동하는 링크를 클릭합니다.
3. 새 탭에서 https://tabnabbing.example.com 페이지가 열립니다.
4. https://tabnabbing.example.com 페이지에서 window.opener 프로퍼티를 이용해 기존 웹 페이지의 url을 피싱 목적의 https://fishing.example.com/login 으로 변경합니다.
5. 사용자가 다시 본래의 웹 페이지로 돌아옵니다.
6. 사용자는 로그인이 풀렸다고 착각하고 아이디와 비밀번호를 다시 입력합니다
7. https://fishing.example.com/login은 사용자가 입력한 계정 정보를 탈취한 뒤 다시 본래의 사이트(https://example.com)로 리다이렉트합니다.

## Tabnabbing 공격 방어법

### a 태그에 rel="noreferrer" 속성을 추가한다

- a 태그의 rel 속성 값으로 `noopener`나 `noreferrer`를 지정하면 새 탭에 표시된 웹 사이트에서 `window.opener` 프로퍼티에 접근 할 수 없게 됩니다.
- `noopener` 값의 경우 이름 그대로 새 탭에서 window.opener에 접근 못 하게 하고 `noreferrer` 값의 경우 새 탭에서 referrer 정보와 window.opener에 접근 못 하게 합니다.
- `rel="noopener"` 속성을 쓰면 ie나 사파리 10버전 이하에서는 정상적으로 작동 하지 않고, `rel="noopener noreferrer"`의 경우 파이어폭스 33 ~ 35버전에서 정상적으로 작동 하지 않기 때문에 `rel="noreferrer"`를 쓰는 것이 제일 브라우저 지원 범위가 넓습니다.

### Reference

- https://github.com/yannickcr/eslint-plugin-react/issues/2022#issuecomment-526320768
