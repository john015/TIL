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

## CSS Clearfix란?

- float된 자식 엘리먼트가 부모 엘리먼트의 높이에 영향을 주지않아 레이아웃이 깨질수가있다.
- 그래서 float된 자식 엘리먼트의 높이를 부모 엘리먼트에 반영하도록 대응하는 방법을 clearfix라고 한다.
- 부모요소를 position: relative로 설정한다.
- 부모요소를 display: inline-block로 설정한다.
- 부모요소를 overflow: auto 또는 hidden으로 설정한다.

## 이미지 스프라이트(Image Sprite)란?

- 이미지 스프라이트는 여러개의 이미지를 합쳐서 하나의 이미지로 만들고 이를 잘라 사용하는 방식이다.
- 한 페이지에 5개의 이미지 리소스가 필요한 경우 5번의 http 요청이 필요하지만 이미지 스프라이트를 사용하게 되면 1번의 http 요청으로 이미지를 다 받아올 수 있다.

## Image Replacement란?

- Image Replacement(IR)이란 웹 접근성을 준수하여 시각장애인에게(이미지를 볼 수 없는 상황) 대체 텍스트를 제공하는 방법이다.
- text-indent를 사용하는 방법과 대체 텍스트요소의 width와 height를 0으로 설정하는 방법이 있다.

```html
<!-- text-indent를 사용하는 방식 -->
<h1
  style="width: 300px; height: 150px; background-image: url('/logo.png'); text-indent: -9999;"
>
  네이버
</h1>

<!-- 대체 텍스트요소의 width와 height를 0으로 설정하는 방식 -->
<h1 style="width: 300px; height: 150px; background-image: url('/logo.png');">
  <span style="width: 0px; height: 0px;">네이버</span>
</h1>
```

## 일반적으로 보이지 않고 스크린 리더에서만 보이게 하는법

- 1. display:none;
- 2. visibility:hidden;
- 3. width: 0; height: 0;
- 4. text-indent: -9999;
