## 서버 데몬 안쓰고 수동으로 실행시킬떄

```sh
postgres -D /usr/local/var/postgres
```

## Postgre SQL shell 진입

```sh
psql [스키마명]
```

## DB 생성

```sh
CREATE DATABASE database_name;
```

## DB 목록 출력

```sh
SELECT datname FROM pg_database;
# or
\l
```

## DB 선택

```sh
\c database_name
```

##테이블 목록 출력

```sh
  \dt
```

## Postgre shell 종료

```sh
  \q
```
