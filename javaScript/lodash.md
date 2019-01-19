Lodash Methods들중 괜찮아 보이는거 정리

## \_.chunk

2 번째 아규먼트로 받은 숫자만큼 배열을 나눠줌

```javascript
\_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

\_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

## \_.intersection

파라미터 배열들에 공통적으로 있는 값만 배열로 리턴해줌 By,with 도 가능함

```javascript
\_.intersection([2, 1], [2, 3]);
// => [2]
```

## \_.difference

첫번째 아규먼트로 받은 배열이랑 다음 아규먼트로 받은 배열이랑 비교를해서 첫번째 배열에만 있는 값을 배열로 리턴해줌

```javascript
\_.difference([2, 1, 5], [2, 3]);
// => [1, 5]
```

## \_.differenceBy

difference 랑 비슷하지만 마지막 아규먼트로 iteratee(루프의 기반 값을 받음)

```javascript
\_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
//반올림을 하여서 비교 => [1.2]

// The `_.property` iteratee shorthand.
\_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
//객체의 x 값을 기준으로 비교 => [{ 'x': 2 }]
```

## \_.differenceWith

3 번째아규먼트로 lodash 함수를 사용해서 differenceBy 처럼 사용함

```javascript
var objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }]

_.differenceWith(objects, [{ x: 1, y: 2 }], _.isEqual)
// => [{ 'x': 2, 'y': 1 }]
```

## \_.findIndex

해당 규칙에 해당하는 인덱스를 앞부터 시작해서 반환함

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

var users = [

{ 'user': 'barney', 'active': false },

{ 'user': 'fred', 'active': false },

{ 'user': 'pebbles', 'active': true }

];

\_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0

// The `_.matches` iteratee shorthand.
\_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1

// The `_.matchesProperty` iteratee shorthand.
\_.findIndex(users, ['active', false]);
// => 0

// The `_.property` iteratee shorthand.
\_.findIndex(users, 'active');
// => 2
```

## \_.findLastIndex(

해당 규칙에 해당하는 인덱스를 뒤부터 시작해서 반환함

```javascript
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];

var users = [

{ 'user': 'barney', 'active': true },

{ 'user': 'fred', 'active': false },

{ 'user': 'pebbles', 'active': false }

];

\_.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2

// The `_.matches` iteratee shorthand.
\_.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0

// The `_.matchesProperty` iteratee shorthand.
\_.findLastIndex(users, ['active', false]);
// => 2

// The `_.property` iteratee shorthand.
\_.findLastIndex(users, 'active');
// => 0
```

## Todo

sorted까지
