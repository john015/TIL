# 선택자

## 조상자손 선택자

- ul 안에 모든 il 을 선택

```
ul li{color:red}
```

## 부모 자식 선택자

- ul 바로 밑에있는 li 만 선택

```
ul>li{color:red}
```

## 동시 선택자

- 둘다 선택

```
li,ul{color:red}
```

## 속성 선택자

- 지정된 어트리뷰트를 갖는 모든 요소를 선택

```
ul[attr] { color: red; }
```

## 인접 형제 선택자

- li 바로 뒤 에있는 ul 를 선택

```
li+ul{color:red}
```

## 일반 형제 선택자

- li 뒤 에있는 ul 를 모두 선택

```
li~ul{color:red}
```

## 가상 클래스 선택자

- :link - 방문한 적이 없는 링크
- :visited - 방문한 적이 있는 링크
- :hover - 마우스를 롤오버 했을때
- :active - 마우스를 클릭했을때

```
li:hover{color:red}
```

## \*선택자

- 모든 엘리먼트들을 다 선택함

# 속성

## 캐스케이딩

- CSS 우선순위 순서 : style 속성 > id 선택자 > class 선택자 > 태그선택자
  <br> !important를 넣으면 우선순위 제일높아짐

## NTH-CHILD(N)과 NTH-OF-TYPE(N)의 차이점

http://blog.hivelab.co.kr/enth-childn%EA%B3%BC-enth-of-typen%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90/