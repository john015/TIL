# MVC pattern

<img src="https://t1.daumcdn.net/cfile/tistory/9911A0445B976CAB03" />

- MVC는 model view controller의 약자로 MVC 패턴의 주 목적은 Bussiness logic과 Presentation logic을 분리하기 위함이다.
- model은 비즈니스 로직 및 데이터를 처리하고
- view는 사용자에게 제공되어 보여지는 UI로직을 처리한다.
- controller는 model과 view사이의 상호작용을 관리한다.
- 모든 입력은 Controller 에서 처리된다. 입력이 Controller로 들어오면 Controller는 입력에 해당하는 Model을 조작(업데이트)하고, Model을 나타내어줄 View를 선택한다.
- Controller는 View와 Model을 알지만 View와 Model은 서로를 모른다(독립적).
- Controller는 View를 선택할수 있기 때문에 하나의 Controller가 여러개의 View를 선택하여 Model을 나타내어 줄 수 있다.
- 이때 Controller는 View를 선택만하고 업데이트를 시켜주지 않기때문에 View는 Model을 이용하여 업데이트 하게된다.
- mvc패턴은 View와 Model이 서로 의존적이기때문에 프로젝트가 커질경우 복잡해지고 유지보수하기 어려워지면서 Controller가 처리하는 로직이 많아지기때문에 최근에는 주로 사용되지 않는다.
