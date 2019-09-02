
# Query

서버에서 데이터 가져오기(fetch)를 할떄 사용(rest API에서 get)

## Fields

```javascript
{
  hero {
    name
  }
}
```

hero객체 안의 name을 요청

## Arguments

```javascript
{
  hero(id: 1) {
    name
  }
}
```

## Aliases

```javascript
{
  empireHero: hero(episode: EMPIRE) {
    name
  }
  jediHero: hero(episode: JEDI) {
    name
  }
}
```

같은 query를 여러번 요청해야될경우 alias를 써서 요청

## Variables

```javascript
query HeroNameAndFriends($episode: Episode = EMPIRE) {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}
```

- 동적으로 인자에 값을 전달할땐 변수를 사용
- 타입 선언 다음에 기본값을 명시하여 쿼리의 변수에 기본값을 할당할 수 있음

## Fragments

```javascript
query HeroComparison($first: Int = 3) {
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}
​
fragment comparisonFields on Character {
  name
  friendsConnection(first: $first) {
    totalCount
    edges {
      node {
        name
      }
    }
  }
}
```

중복되는 코드가 있을경우 fragment를 사용하여 제거

## Directives

```javascript
query Hero($episode: Episode, $withFriends: Boolean!) {
  hero(episode: $episode) {
    name
    friends @include(if: $withFriends) {
      name
    }
  }
}
```

- @include(if: Boolean): 인자가 true 인 경우에만 이 필드를 결과에 포함합니다.
- @skip(if: Boolean) 인자가 true 이면 이 필드를 건너뜁니다.
