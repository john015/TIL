# Event Loop

- 브라우저는 단일 쓰레드(single-thread) 이벤트 드리븐(event-driven) 방식으로 동작한다.
- 쓰레드가 하나밖에 없기때문에 하나의 작업(task)만을 처리할 수 있다.
- 하지만 실제로 동작하는 웹 애플리케이션은 많은 task가 동시에 처리되는 것처럼 느껴진다.
- 이처럼 자바스크립트의 동시성(Concurrency)을 지원하는 것이 바로 이벤트 루프(Event Loop)이다

<img src="https://user-images.githubusercontent.com/32455422/85952962-d310ec00-b9a7-11ea-8d21-f4ac2cd74735.png">

### Call Stack(호출 스택)

- 작업이 요청되면(함수가 호출되면) 요청된 작업은 순차적으로 Call Stack에 쌓이게 되고 순차적으로 실행된다.
- 자바스크립트는 단 하나의 Call Stack을 사용하기 때문에 해당 task가 종료하기 전까지는 다른 어떤 task도 수행될 수 없다.(Run-to-completion)

### Heap

- 동적으로 생성된 오브젝트(객체)들은 힙 내부에 할당함.
- 힙은 거의 구조화되지 않은 영역(unstructured)의 메모리입니다. 변수와 객체들의 모든 메모리 할당이 여기서 일어나게 된다.

이와 같이 자바스크립트 엔진은 단순히 작업이 요청되면 Call Stack을 사용하여 요청된 작업을 순차적으로 실행할 뿐이다.
앞에서 언급한 동시성(Concurrency)을 지원하기 위해 필요한 비동기 요청(이벤트를 포함) 처리는 자바스크립트 엔진을 구동하는 환경에서 담당한다.

### Task Queue(Event Queue)

Timer 함수(`setTimeout`, `setInterval`), DOM 이벤트 리스너 등등의 콜백 함수가 보관되는 영역

### Microtask Queue

Promise 객체의 `.then`/`.catch`/`.finally` 콜백 함수가 보관되는 영역

### Animation Frame

`requestAnimationFrame`의 콜백 함수가 보관되는 영역

### Event Loop(이벤트 루프)

- Call Stack 내에서 현재 실행중인 task가 있는지 그리고 각각의 Queue들에 task가 있는지 반복하여 확인한다.
- 만약 Call Stack이 비어있다면 Queue 내의 task를 Call Stack으로 이동시키고 실행한다.
- Chrome기준으 Microtask Queue => Animation Frame => Event Queue 순서로 queue안에 들어있는 task들을 확인하고 만약 있다면 Call Stack에 추가한다.

## Reference

- https://poiemaweb.com/js-event#2-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84event-loop%EC%99%80-%EB%8F%99%EC%8B%9C%EC%84%B1concurrency
- https://meetup.toast.com/posts/89
- https://engineering.linecorp.com/ko/blog/dont-block-the-event-loop/
- http://sculove.github.io/blog/2018/01/18/javascriptflow/
