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
  logo
</h1>

<!-- 대체 텍스트요소의 width와 height를 0으로 설정하는 방식 -->
<h1 style="width: 300px; height: 150px; background-image: url('/logo.png');">
  <span style="width: 0px; height: 0px;">logo</span>
</h1>
```

## 일반적으로 보이지 않고 스크린 리더에서만 보이게 하는법

- display:none;
- visibility:hidden;
- width: 0; height: 0;
- text-indent: -9999;
- position; absolute; left: -99999px;

## @media print이란?

- 인쇄하면에서 스타일을 지정하기 위해선 미디어쿼리의 print 속성을 사용하여 스타일을 지정할 수 있다.

## 가상 요소 셀랙터(Pseudo-Element Selector)란?

- pseudo-element Selector란 element의 특정 부분을 스타일하는데 사용한다.

  | pseudo-element | Description                                                                      |
  | -------------- | -------------------------------------------------------------------------------- |
  | ::first-letter | 콘텐츠의 첫글자를 선택한다.                                                      |
  | ::first-line   | 콘텐츠의 첫줄을 선택한다. BFC에만 적용할 수 있다.                                |
  | ::after        | 콘텐츠의 뒤에 위치하는 공간을 선택한다. 일반적으로 content 속성과 같이 사용된다. |
  | ::before       | 콘텐츠의 앞에 위치하는 공간을 선택한다. 일반적으로 content 속성과 같이 사용된다. |
  | ::selection    | 드래그한 콘텐츠를 선택한다. iOS Safari 등 일부 브라우저에서 동작 안한다.         |

## box model이란?

- 기본값인 content-box의 경우는 element의 width나 height를 설정할 경우 해당 element의 content width/height 값을 설정하기때문에 element의 padding/border값이 설정되어있을경우 원하는 width랑 다를수있다.
- 그렇기때문에 padding의 영향을 안받을려면 box-sizing: border-box;로 설정하여야 한다.

## \* { box-sizing: border-box; }의 장점은?

- element의 크기(width, height)를 설정하면 컨텐츠의 표시영역을 입력한 크기값과 동일하게 보여준다.
- 그래서 padding 값이나 border 값이 늘어나면 element의 크기가 의도한것보다 커지는 문제가 발생할 수 있다.
- box-sizing: border-box;로 설정하게 되면 padding 값이나 border 값이 늘어나도 element의 크기가 변하지 않으며 컨텐츠의 표시영역이 줄어들어 일관된 사이즈를 유지할 수 있습니다.

## 반응형(Responsive) 디자인 vs 적응형(Adaptive) 디자인

- 반응형 웹 디자인은 mediaquery를 사용해 화면 해상도를 감지한뒤 화면 크기에 맞게 디자인을 하는것이다.
- 적응형 웹 디자인은 서버또는 브라우저에서 기기나 해상도를 감지한뒤 화면 크기에 맞는 디자인이 적용된 페이지로 리다이렉션 시키는것이다.

## positon vs translate

translate를 사용해서 엘리먼트의 위치를 변경하면 composite만 일어나지만 left/right/top/bottom을 사용하여 위치를 변경하면 reflow(layout)가 일어난다.

## reflow를 피하거나 최소화하는 방법

reflow란 생성된 엘리먼트의 레이아웃(너비, 높이 등) 변경 시 영향받는 모든 노드(자식, 부모)의 수치를 다시 계산하여 렌더 트리를 재생성하는 작업이다.
reflow가 자주 발생하면 성능이 안좋아진다.

### 1. 클래스 변화에 따른 스타일 변화를 원할 경우, 최대한 DOM 구조 상 끝단에 위치한 노드에 추가한다.

### 2. 애니메이션이 들어간 엘리먼트는 가급적 position: fixed 또는 position: absolute로 지정한다.

위치 이동을 구현한 애니메이션(넓이나 높이값 변경 등)은 reflow가 짧은 시간 내 반복적으로 일어나게 됩니다. 그래서 사용하지 않는 것이 가장 바람직하나 반드시 사용해야 한다면 애니메이션이 들어간 요소에 position: absolute 혹은 position: fixed 속성을 적용합니다. 다른 요소에는 영향을 끼치지 않으므로 페이지 전체가 아닌 해당 요소만 reflow가 발생합니다.

### 3. JS를 통해 스타일 변화를 주어야 할 경우, 가급적 한번에 처리한다.

style 객체를 여러번 호출해 스타일 변화를 주지말고 CSS 정의된 class를 통해 한번에 변화를 적용해준다.

### 4. 인라인 스타일을 최대한 배제합니다.

위의 내용과 중복되며, reflow 비용을 줄이는 것 이외에 코드 가독성도 높일 수 있다.

### 5. 테이블 레이아웃을 피한다.

### 6. CSS 하위선택자는 필요한 만큼만 사용한다.

CSS 규칙은 오른쪽에서 왼쪽으로 이동하면서 읽기때문에 불필요한 선택자를 사용하는 것은 성능을 저하시킬 수 있다.

## will-change이란

will-change는 변화가 예상되는 요소를 브라우저에게 미리 알려줍니다. 브라우저는 실제 요소가 변화되기 전에 적절하게 최적화를 할 수 있습니다. 큰 비용이 드는 변화도 최적화로 인해 페이지의 반응성을 증가시킬 수 있습니다.

하지만 너무 많은 요소에 will-change요소를 사용하면 오히려 성능이 더 안좋아질수도 있다.
