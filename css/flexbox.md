# FlexBox

## Flex 컨테이너 선언

display 속성을 flex나 inline-flex으로 설정합니다.

```css
.parent {
  display: flex; /* BFC */
  display: inline-flex; /* IFC */
}
```

## Flex 컨테이너 속성

### flex-direction

해당 CSS 속성은 flex 컨테이너안의 요소들이 정렬될 방향을 지정하는 속성입니다.

기본값은 `row`이며 4개의 값을 가질 수 있습니다.

- row: 요소들을 텍스트의 방향과 동일하게 정렬합니다.
- row-reverse: 요소들을 텍스트의 반대 방향으로 정렬합니다.
- column: 요소들을 위에서 아래로 정렬합니다.
- column-reverse: 요소들을 아래에서 위로 정렬합니다.

### justify-content

해당 CSS 속성은 주축(flex-direction)에 따라 flex요소들의 행을 정렬하는 방식을 지정합니다.

flex-direction이 row일경우 가로를 정렬하며, column일경우 세로를 정렬합니다.

기본값은 `flex-start`이며 5개의 값을 가질 수 있습니다.

- flex-start: 요소들을 컨테이너의 왼쪽으로 정렬합니다.
- flex-end: 요소들을 컨테이너의 오른쪽으로 정렬합니다.
- center: 요소들을 컨테이너의 가운데로 정렬합니다.
- space-between: 요소들 사이에 동일한 간격을 둡니다.
- space-around: 요소들 주위에 동일한 간격을 둡니다.

### align-items

해당 CSS 속성은 주축(flex-direction)에 따라 flex요소들의 열을 정렬하는 방식을 지정합니다.

flex-direction이 row일경우 세로를 정렬하며, column일경우 가로를 정렬합니다.

기본값은 `stretch`이며 5개의 값을 가질 수 있습니다.

- flex-start: 요소들을 컨테이너의 꼭대기로 정렬합니다.
- flex-end: 요소들을 컨테이너의 바닥으로 정렬합니다.
- center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
- baseline: 요소들을 컨테이너의 시작 위치에 정렬합니다.
- stretch: 요소들을 컨테이너에 맞도록 늘립니다.

### flex-wrap

해당 CSS 속성은 flex 요소들을 여러행에 나열 되도록 할 때 사용합니다.

flex-direction과 flex-wrap이 자주 같이 사용되기 때문에, flex-flow가 이를 대신할 수 있습니다. 이 속성은 공백문자를 이용하여 두 속성의 값들을 인자로 받습니다.

기본값은 `nowrap`이며 3개의 값을 가질 수 있습니다.

- nowrap: 모든 요소들을 한 줄에 정렬합니다.
- wrap: 요소들을 여러 줄에 걸쳐 정렬합니다.
- wrap-reverse: 요소들을 여러 줄에 걸쳐 반대로 정렬합니다.

```css
.parent {
  display: flex;
  flex-flow: wrap column;
}
```

### align-content

해당 CSS 속성은 flex-wrap을 wrap으로 설정하여 요소들이 여러행에 나열 될 때 행 사이의 간격을 지정합니다.

기본값은 `stretch`이며 6개의 값을 가질 수 있습니다.

- flex-start: 여러 행들을 컨테이너의 꼭대기에 정렬합니다.
- flex-end: 여러 행들을 컨테이너의 바닥에 정렬합니다.
- center: 여러 행들을 세로선 상의 가운데에 정렬합니다.
- space-between: 여러 행들 사이에 동일한 간격을 둡니다.
- space-around: 여러 행들 주위에 동일한 간격을 둡니다.
- stretch: 여러 행들을 컨테이너에 맞도록 늘립니다.

## Flex 요소 속성

### order

해당 CSS 속성은 해당 요소의 배치 순서를 지정합니다.

기본값은 `0`이며 값이 클수록 뒤에 배치됩니다.

### align-self

해당 CSS 속성은 align-items와 동일하게 동작하지만 해당 요소에만 정렬이 적용됩니다.

flex-direction이 row일경우 세로를 정렬하며, column일경우 가로를 정렬합니다.

기본값은 `stretch`이며 5개의 값을 가질 수 있습니다.

- flex-start: 요소들을 컨테이너의 꼭대기로 정렬합니다.
- flex-end: 요소들을 컨테이너의 바닥으로 정렬합니다.
- center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬합니다.
- baseline: 요소들을 컨테이너의 시작 위치에 정렬합니다.
- stretch: 요소들을 컨테이너에 맞도록 늘립니다.

### flex-grow

해당 CSS 속성은 해당 요소가 차지하는 공간의 비율를 지정합니다.

만약 box의 flex-grow는 2이고 box1의 flex-grow는 1이면 2:1의 비율로 공간을 차지합니다.

기본값은 `0`입니다.

### flex-basis

해당 CSS 속성은 해당 요소의 width를 지정합니다.

flex-basis가 100px이면 100px만큼 공간을 차지합니다.

기본값은 `auto`입니다.

### flex-shrink

flex-shrink 속성은 컨테이너의 공간이 부족할 때 각 항목의 사이즈를 줄이는 방법을 정의합니다.

만약 flex 컨테이너가 flex 항목을 모두 포함할 만큼 넉넉한 공간을 갖고 있지 않고 flex-shrink 값이 양수이면 flex 항목은 flex-basis에 지정된 크기보다 작아집니다.

또한, flex-grow 속성과 마찬가지로 더 큰 flex-shrink 값을 갖는 항목의 사이즈가 더 빨리 줄어듭니다.
