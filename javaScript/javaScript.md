## javascript typecheck 할때

'''
toString.call(check 하고싶은거)
'''

## substr() , slice() 차이

substr()은 시작부터 추출 길이
slice()은 시작 부터 끝 인덱스
substring()은 slice() 랑 비슷하지만 음수 파라미터 가 안됨

'''
const target = 'hello world'
const substring = target.substring(2,5) // 2 부터 5 전까지 "llo"
const slice = target.slice(2,5) // 2 부터 5 전까지 "llo"
const substr = target.substr(2,5) // 2 부터 5 글자 "llo w"
'''

## function 유효범위

javascript function 은 렉시컬 스코프를 가지고 있어 소스코드가 작성된 그 문맥에서 결정된다.

'''
const x = 'global'

function a () {
    console.log(x)
}

function b () {
    const x = 'local'
    a()
}
a() //global
b() //global
'''

## apply vs call

apply : 2번째 파라미터로 배열을 받음
call : 파라미터를 쭉나열함

'''
var val1 = 30
var val2 = 50
const obj = {
    val1: 40,
    val2: 90,
    sum (a,b) {
        return this.val1 + this.val2 + a + b;
    }
}
console.log(obj.sum(0,100)) //230
console.log(obj.sum.call(this, 0, 100)) //180
console.log(obj.sum.apply(this, [0, 100])) //180
```