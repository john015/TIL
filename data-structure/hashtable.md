# HashTable

HashTable은 key에 Value를 저장하는 데이터 구조로 get(key)의 동작이 O(1)의 시간복잡도로 수행된다.

동작방식은 key를 hashing(hashFunction(key) % bucketSize)해서 index값을 구하고 내부의 array의 index에 value를 저장한다.

이런 형식으로 data를 저장하면, key에 대한 data를 찾을때, hashing 한번만 수행하면 array내에 저장된 index 위치를 찾아낼 수 있기 때문에, data 저장과 삭제가 빠르다(O(1)).

하지만 hashFunction(key) / bucketSize 값이 중복이 될수가 있기때문에 Linked-list를 사용하거나 array를 사용해서 충돌을 해결할 수 있다.

```javascript
class HashTable {
  constructor(bucketSize = 1024) {
    this._bucketSize = bucketSize
    this._data = new Array(bucketSize)
  }

  getHashKey(key) {
    const h = key
      .split('')
      .reduce((acc, cur, i) => acc + cur.charCodeAt(0) * (i + 1), 0)
    return h % this._bucketSize
  }

  set(key, value) {
    if (typeof key !== 'string') {
      key = JSON.stringify(key)
    }
    const hashKey = this.getHashKey(key)
    const bucket = this._data[hashKey]
    if (!bucket) {
      return (this._data[hashKey] = [[key, value]])
    }
    const idx = bucket.findIndex(([storedKey]) => key === storedKey)
    if (idx === -1) {
      return bucket.push([key, value])
    }
    bucket[idx][1] = value
  }

  get(key) {
    if (typeof key !== 'string') {
      key = JSON.stringify(key)
    }
    const bucket = this._data[this.getHashKey(key)]
    if (bucket) {
      const data = bucket.find(([storedKey]) => key === storedKey)
      return data ? data[1] : undefined
    }
    return undefined
  }
}

const ht = new HashTable()
ht.set({ x: 210 * 2 }, 420)
ht.set({ x: 210 * 2 }, 1)
ht.set([1, 2, 3], 2)
ht.set('cba', 3)

ht.get({ x: 420 }) // 1
ht.get([2, 4, 6].map(x => x / 2)) // 2
ht.get('cba') // 3
```
