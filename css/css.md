## 선택자

### 조상자손 선택자

- ul 안에 모든 il 을 선택

```
ul li{color:red}
```

### 부모 자식 선택자

- ul 바로 밑에있는 li 만 선택

```
ul>li{color:red}
```

### 동시 선택자

- 둘다 선택

```
li,ul{color:red}
```

### 속성 선택자

- 지정된 어트리뷰트를 갖는 모든 요소를 선택

```
ul[attr] { color: red; }
```

### 인접 형제 선택자

- li 바로 뒤 에있는 ul 를 선택

```
li+ul{color:red}
```

### 일반 형제 선택자

- li 뒤 에있는 ul 를 모두 선택

```
li~ul{color:red}
```

### 가상 클래스 선택자

- :link - 방문한 적이 없는 링크
- :visited - 방문한 적이 있는 링크
- :hover - 마우스를 롤오버 했을때
- :active - 마우스를 클릭했을때

```
li:hover{color:red}
```

### \*선택자

- 모든 엘리먼트들을 다 선택함

## BFC(Block Formatting contexts) vs IFC(Inline Formatting contexts)

- BFC는 context의 height값 만큼 페이지의 width를 다 차지하고 수직으로 쌓인다.
- IFC는 context의 width만큼 페이지의 width를 차지하고 수평으로 쌓인다.

## NTH-CHILD(N)과 NTH-OF-TYPE(N)의 차이점

- E:nth-child(n)는 부모 엘리먼트의 모든 자식 엘리먼트중 n번째 엘리먼트가 E 엘리먼트인경우 스타일이 적용된다.
- E:nth-of-type(n)는 부모 엘리먼트의 자식 엘리먼트중 n번째 E 엘리먼트에게 스타일이 적용된다.
  http://blog.hivelab.co.kr/enth-childn%EA%B3%BC-enth-of-typen%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90/

## CSS Clearfix란?

- float된 자식 엘리먼트가 부모 엘리먼트의 높이에 영향을 주지않아 레이아웃이 깨질수가있다.
- 그래서 float된 자식 엘리먼트의 높이를 부모 엘리먼트에 반영하도록 대응하는 방법을 clearfix라고 한다.
- 부모요소를 position: relative로 설정한다.
- 부모요소를 display: inline-block로 설정한다.
- 부모요소를 overflow: auto 또는 hidden으로 설정한다.
