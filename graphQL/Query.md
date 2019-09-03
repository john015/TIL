# Query

서버에서 데이터 가져오기(fetch)를 할떄 사용합니다.(rest API에서 get)

## Fields

```javascript
{
  hero {
    name
  }
}
```

hero 루트 필드에서 name 필드 값을 요청합니다.

```javascript
{
  hero {
    name
    age
  }
}
```

hero 루트 필드에서 name, age 필드 값을 요청합니다.

## Arguments

GraphQL에서는 각 필드가 스키마에 정의된 규칙에 따라 0개 이상의 인자를 가질 수 있습니다.

```javascript
{
  hero(id: 1) {
    name
  }
}
```

id가 1인 hero의 name 필드 값만 요청합니다.

## Aliases

```javascript
{
  empireHero: hero(episode: "EMPIRE") {
    name
  }
  jediHero: hero(episode: "JEDI") {
    name
  }
}
```

같은 query를 여러번 요청해야 될 경우 alias를 써서 요청할 수 있습니다.

## Variables

```javascript
query HeroNameAndFriends($episode: Episode = "JEDI") {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}
```

- 동적으로 인자에 값을 전달할땐 변수를 사용 할 수 있습니다.
- 타입 선언 다음에 기본값을 명시하여 쿼리의 변수에 기본값을 할당할 수 있습니다.
- \$episode hero의 이름과 친구들의 이름을 요청

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

중복되는 코드가 있을경우 fragment를 사용하여 제거 할 수 있습니다.

fragment를 선언 할 때 on 뒤에 data type을 지정해줘야합니다.

필드의 반환값이 해당 data type일 경우에만 실행 됩니다.

## Inline-fragment

```javascript
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
    ... on Human {
      height
    }
  }
}
```

반환 되는 hero 객체의 타입에 따라서 요청하는 필드의 조건을 바꿔야 할경우 인라인 프래그먼트를 사용합니다.

hero의 타입이 Droid일 경우 primaryFunction값을 반환하고 Human일경우 height값을 반환합니다.

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

- @include(if: Boolean): Boolean값이 true 인 경우에만 필드를 결과에 포함합니다.
- @skip(if: Boolean) Boolean값이 true면 필드를 건너뜁니다.
