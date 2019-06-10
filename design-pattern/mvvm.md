# MVVM pattern

<img src="https://t1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/0biW4YNB0bAVV4zzOuNBsdV0Fz8.png" />

- MVVM는 model view viewModel의 약자로 목적과 model, view의 역할은 다른 디자인 패턴들과 동일하지만 Controller대신 viewModel을 사용한다 또한 action이 view를 통해 들어오게된다.
- viewModel이란 해당 View를 표현하기 위해 만든 Model이다 view와 viewModel은 binding되어 있다.
- Model이 변경되면 해당하는 ViewModel을 이용하는 View가 자동으로 업데이트된다.
- MVVM 패턴의 가장 큰 장점은 Command 패턴과 Data Binding으로 의존성이 사라진다.

## flow

- View로 입력이 들어오면 Command 패턴으로 ViewModel에 명령을 한다.
- ViewModel은 입력이 들어온 데이터 처리를 Model에 요청한다.
- Model은 ViewModel이 요청한 데이터처리를 한뒤 응답한다.
- ViewModel은 응답 받은 데이터를 가공해서 저장한다.
- View는 ViewModel과의 Data Binding으로 인해 자동으로 갱신된다.

https://brunch.co.kr/@oemilk/113
