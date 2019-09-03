# Mutation

서버의 데이터를 생성, 수정, 삭제할 때 사용합니다.(POST, PUT, PATCH, DELETE)

Query와 다른점은 Mutation은 하나의 요청에서 두 개의 Mutation 요청을 보내면 첫 번째는 두 번째 요청 전에 실행이 완료되는 것이 보장됩니다.

## Mutation

```javascript
mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}

// variables
{
  "ep": "JEDI",
  "review": {
    "stars": 5,
    "commentary": "This is a great movie!"
  }
}
```

`CreateReviewForEpisode` mutation이 리뷰를 생성하고 생성한 리뷰를 반환하는 mutation일때, 위 쿼리는 리뷰를 생성하고 생성한 리뷰의 stars와 commentary를 반환합니다.

만약 리턴될 객체의 타입을 모르는 상황이 발생되면, 메타 필드인`__typename`를 요청하여 그 시점에서 객체 타입의 이름을 얻을 수 있습니다.
