# DOM 조회

## Node.parentNode: HTMLElement

부모 노드를 탐색한다.

## Node.firstChild: HTMLElement

첫 번째 자식 노드를 탐색한다.

IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급하기 때문에 Element를 얻을려면 Node.firstElementChild를 사용 해야 한다.

## Node.lastChild: HTMLElement

마지막 번째 자식 노드를 탐색한다.

IE를 제외한 대부분의 브라우저들은 요소 사이의 공백 또는 줄바꿈 문자를 텍스트 노드로 취급하기 때문에 Element를 얻을려면 Node.lastElementChild를 사용 해야 한다.

## Node.hasChildNodes(): Boolean

자식 노드가 있는지 확인한다.

## Node.childNodes: NodeList

자식 노드의 컬렉션을 반환한다. 텍스트 요소를 포함한 모든 자식 요소를 반환한다.

## Node.children: NodeList

자식 노드의 컬렉션을 반환한다. 자식 요소 중에서 Element type 요소만을 반환한다.

## Node.previousSibling: HTMLElement

이전 형제 노드를 탐색한다. text node를 포함한 모든 형제 노드를 탐색한다.

## Node.nextSibling: HTMLElement

다음 형제 노드를 탐색한다. text node를 포함한 모든 형제 노드를 탐색한다.

## Node.previousElementSibling: HTMLElement

이전 형제 엘리먼트를 탐색한다.

## Node.nextElementSibling: HTMLElement

다음 형제 엘리먼트를 탐색한다.

## Node.nodeName: String

노드의 html tag Name을 반환한다(대문자)

## Node.nodeType: Number

노드의 type을 반환한다.

[타입 참고](https://developer.mozilla.org/ko/docs/Web/API/Node/nodeType#Constants)

## Node.textContent: Strig

해당 노드의 텍스트 콘텐츠를 탐색한다.

## Node.innerHTML

해당 요소의 모든 자식 요소를 포함하는 모든 콘텐츠를 하나의 문자열로 취득할 수 있다. 이 문자열은 마크업을 포함한다.

## Node.hasAttribute(attribute): Boolean

지정한 어트리뷰트를 가지고 있는지 검사한다.

## Node.getAttribute(attribute): String

해당 어트리뷰트의 값을 취득한다.

## Node.setAttribute(attribute, value): Undefined

해당 어트리뷰트와 값을 설정한다.

## Node.removeAttribute(attribute): Undefined

해당 어트리뷰트를 제거한다.

# DOM 조작

innerHTML 프로퍼티를 사용하지 않고 새로운 콘텐츠를 추가할 수 있는 방법은 DOM을 직접 조작하는 것이다. 이 방법은 다음의 수순에 따라 진행한다.

- 요소 노드 생성: createElement() 메소드를 사용하여 새로운 요소 노드를 생성한다. createElement() 메소드의 인자로 태그 이름을 전달한다.
- 텍스트 노드 생성: createTextNode() 메소드를 사용하여 새로운 텍스트 노드를 생성한다. 경우에 따라 생략될 수 있지만 생략하는 경우, 콘텐츠가 비어 있는 요소가 된다.
- 생성된 요소를 DOM에 추가: appendChild() 메소드를 사용하여 생성된 노드를 DOM tree에 추가한다. 또는 removeChild() 메소드를 사용하여 DOM tree에서 노드를 삭제할 수도 있다.

```javascript
// 태그이름을 인자로 전달하여 요소를 생성
const newElem = document.createElement('li')

// 텍스트 노드를 생성
const newText = document.createTextNode('Beijing')

// 텍스트 노드를 newElem 자식으로 DOM 트리에 추가
newElem.appendChild(newText)

const container = document.querySelector('ul')

// newElem을 container의 자식으로 container 맨밑에 추가.
container.appendChild(newElem)

// newElem을 container의 자식으로 target Element 앞에 삽입
container.insertBefore(newElem, target)

const removeElem = document.getElementById('one')

// container의 자식인 removeElem 요소를 DOM 트리에 제거한다.
container.removeChild(removeElem)
```

## Node.insertAdjacentHTML(position, string)

인자로 전달한 텍스트를 HTML로 파싱하고 그 결과로 생성된 노드를 DOM 트리의 지정된 위치에 삽입한다. 첫번째 인자는 삽입 위치, 두번째 인자는 삽입할 요소를 표현한 문자열이다. 첫번째 인자로 올 수 있는 값은 아래와 같다.

- ‘beforebegin’: Node의 앞에 삽입한다.
- ‘afterbegin’: Node 내부의 맨 처음에 삽입한다.
- ‘beforeend’: Node 내부의 맨 뒤에 삽입한다.(appendChild)
- ‘afterend’: Node의 뒤에 삽입한다.

```javascript
const one = document.getElementById('one')

// 마크업이 포함된 요소 추가
one.insertAdjacentHTML('beforeend', '<em class="blue">, Korea</em>')
```
