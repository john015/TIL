# MVP pattern

<img src="https://t1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/1OLd/image/6nRFassnqDBTS-p0qGLSS-FAWT4.png" />

- MVP는 model view presenter 약자로 목적과 model, view의 역할은 다른 디자인 패턴들과 동일하지만 Controller대신 presenter를 사용한다
- View와 Model 은 오로지 Presenter에 의해서만 상호작용을 하게 된다.
- 그로 인해 View-Model 의존성은 없지만 View-Presenter 관계는 서로 강하게 의존한다.
- View-Presenter은 1:1 관계다.
- View는 Presenter를 참조하고, Presenter는 View의 존재를 알고 있다.
- View는 Model의 존재를 모른다.
- Presenter는 Model을 업데이트하고, 원하는 데이터를 가져온다.

## flow

- 모든 입력은 View로 들어온다.
- View에서 Presenter 이벤트를 호출한다.
- Presenter에서 Model에 데이터 처리를 요청한다.
- Model은 Presenter가 요청한 데이터처리를 한뒤 전달한다.
- Presenter에서 전달받은 데이터를 기반으로 View를 업데이트한다.
