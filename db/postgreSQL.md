## 서버 데몬 안쓰고 수동으로 실행시킬떄

```sh
postgres -D /usr/local/var/postgres
```

## Postgre SQL shell 진입시

```sh
psql [스키마명]
```

## DB 목록 출력 (show databases)

```sh
SELECT datname FROM pg_database;
# or
\l
```
