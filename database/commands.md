# Как пользоваться Clickhouse
## Инициировать репозиторий на ВМ
Создать папку для Clickhouse
```commandline
mkdir {проект}/{ветка}/clickhouse/
```

## Поднять контейнер
> Задать **CLICKHOUSE_USER**, **CLICKHOUSE_PASSWORD** дефолтного user, **container_name** (project-getntrends-test-clickhouse)
```commandline
docker run -d \
-p 10011:8123 -p 10012:9000 \
-v $(realpath ./clickhouse/ch_data):/var/lib/clickhouse/ \
-v $(realpath ./clickhouse/ch_logs):/var/log/clickhouse-server/ \
-e CLICKHOUSE_DEFAULT_ACCESS_MANAGEMENT=1 \
-e CLICKHOUSE_USER={login} -e CLICKHOUSE_PASSWORD={password} \
--name {container_name} \
--ulimit nofile=262144:262144 \
clickhouse/clickhouse-server:22.2
```
## Создать роль и пользователя
Создать роль с правами
```sql
CREATE ROLE {role};
GRANT SELECT ON *.* TO {role};
```

Создать пользователя с ролью
```sql
CREATE USER {login} IDENTIFIED WITH sha256_password BY '{password}';
GRANT {role} TO {login};
```





