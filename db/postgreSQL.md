## 서버 데몬 안쓰고 수동으로 실행시킬떄

```
postgres -D /usr/local/var/postgres
```

## Postgre SQL shell 진입시

`psql [스키마명]`

## DB 목록 출력 (show databases)

```
SELECT datname FROM pg_database;
\l
```
