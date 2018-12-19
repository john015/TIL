# HTML5

## IE 조건부 주석

! : 아니다(not) - 예) [if !ie] ie 가 아니라면
lt : 작다(less than) - 예) [if lt ie 9] ie9 보다 작다면
lte : 작거나 같다(less than equal) - 예) [if lte ie 8] ie8 보다 작거나 같다면
gt : 크다(greater than) - 예) [if gt ie 6] ie6 보다 크다면
gte : 크거나 같다(greater than equal) - 예) [if gte ie 7] ie7 보다 크거나 같다
() : 우선처리
& : 그리고(and) - 예) [if (gte ie 7)&(lt ie 9)] ie7 이상이고 ie9 미만이라면
| : 또는(or) - 예) [if (ie 7)|(ie 8)] ie7 이거나 ie8 이라면

```
<!--[if lt IE 9]> <script src="./src/demo.js"> <![endif]--> //ie 9미만
<!--[if lte IE 9]> <script src="./src/demo.js"> <![endif]--> //ie 9이하
```
