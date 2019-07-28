# 트라이(Trie)

- 트라이(Trie)는 문자열에서의 검색을 빠르게 해주는 자료구조이다.
- 트라이를 사용하면 검색하는 단어의 길이가 M일때 O(M)의 시간이 소요된다.

```javascript
class Trie {
  constructor() {
    this.words = 0
    this.prefixes = 0
    this.children = []
  }

  // Insert a string into the Trie
  insert(str, position = 0) {
    if (!str.length) return
    if (position === str.length) {
      return this.words++
    }
    this.prefixes++
    const ch = str[position]
    if (this.children[ch] === undefined) {
      this.children[ch] = new Trie()
    }
    const child = this.children[ch]
    child.insert(str, position + 1)
  }

  // Remove a string from Trie
  remove(str, position = 0) {
    if (position === str.length) this.words--
    if (str.length === 0) {
      return
    }
    this.prefixes--
    const ch = str[position]
    const child = this.children[ch]
    if (child) {
      child.remove(str, position + 1)
    }
  }

  // Trie with a given prefix
  find(str = '') {
    let wordStack = []

    if (this.words > 0) {
      wordStack.push(str)
    }

    for (const ch in this.children) {
      const child = this.children[ch]
      wordStack = wordStack.concat(child.find(str + ch))
    }
    return wordStack
  }

  // Return the autoComplete object
  autoComplete(str, pos = 0) {
    if (!str.length) return {}
    const ch = str[pos]
    const child = this.children[ch]

    if (child === undefined) {
      return {}
    }
    if (pos === str.length - 1) {
      return { prev: str, found: child.find(str) }
    }
    return child.autoComplete(str, pos + 1)
  }
}
```
