## 계수 정렬(counting sort)

먼저 배열을 생성한뒤 생성한 배열에 정렬할 배열의 원소중 제일 큰 수 만큼 0을 넣습니다

배열을 순회하며 각 원소가 몇번 등장했는지 갯수를 생성한 배열에 저장합니다

갯수를 저장한 것을 누적합으로 바꿔줍니다

누적합을 바탕으로 값을 결과에 넣어줍니다

```javascript
function countingSort(array) {
  const max = Math.max(...array)
  const count = new Array(max + 1).fill(0)
  const result = []
  array.forEach(val => {
    count[val]++
  })
  for (let i = 0; i < max; i++) {
    // 누적합을 구합니다.
    count[i + 1] += count[i]
  }
  array.forEach(val => {
    // 누적합이 가리키는 인덱스를 바탕으로 결과에 숫자를  집어넣습니다.
    result[count[val] - 1] = val
    count[val]--
  })
  return result
}

countingSort([1, 3, 2, 4, 11, 2, 6, 4, 11, 1, 7])
```
