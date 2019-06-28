# FlexBox

## Flex 컨테이너 선언

display 속성을 flex나 inline-grid으로 설정합니다.

```css
.parent {
  display: grid; /* BFC */
  display: inline-grid; /* IFC */
}
```

## Grid 컨테이너 속성

### grid-template-rows, grid-template-columns

grid-template-rows 속성은 행을 정의하고, grid-template-columns은 열을 정의합니다.

```css
.wrapper {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-columns: repeat(3, 100px); /* 위 코드와 동일 */
  grid-template-rows: 50px 50px;

  grid-template: 50px 50px / 100px 100px 100px; /* rows / columns 로 축약가능 */
}
```

grid-template-rows에 대해 두 개의 값을 지정 했으므로 50px높이의 두 개의 행을 얻고 grid-template-columns에 대해 세 개의 값을 지정 했으므로 100px 너비의 세 개의 열을 얻었습니다(3 X 2).

### grid-gap

요소들 사이의 간격을 지정합니다.

## Gird 요소 속성

### grid-column, grid-row

이 CSS 속성들은 해당 요소의 위치를 ​​지정하고 크기를 조정합니다.

```css
.item1 {
  grid-column-start: 1; /* 1번째 column에서 시작해서 */
  grid-column-end: 4; /* 4번째 column전까지 차지 */
  grid-column: 1 / 4; /* start / end 로 축약가능 */
}

.item2 {
  grid-row-start: 2; /* 2번째 row에서 시작해서 */
  grid-row-end: 4; /* 4번째 row전까지 차지 */
  grid-row: 2 / 4; /* grid-column과 동일 */
}

.item3 {
  grid-row: 2 / span 2; /* span을 사용하면 span뒤에 나온 숫자만큼(2번째 row부터 2칸의 row) 차지 */
}

.item4 {
  grid-area: 1 / span 3 / 2 / span 2; /* grid-row-start / grid-column-start / grid-row-end  / grid-cloumn-end를 축약 */
}
```

### order

해당 CSS 속성은 해당 요소의 배치 순서를 지정합니다.

기본값은 `0`이며 값이 클수록 뒤에 배치됩니다.

## grid 특징

### fr

fr이란 그리드 컨테이너내 남은 공간 비율 단위입니다.

```css
.grid {
  display: grid;
  grid-template-columns: auto 100px 1fr 2fr;
}
```

3번째 열은 남은 공간중 1/3을 차지하며 4번째 열은 2/3을 차지합니다.
