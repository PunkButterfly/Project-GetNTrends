mkdir clickhouse/

docker run -d \
-p 10011:8123 -p 10012:9000 \
-v $(realpath ./clickhouse/ch_data):/var/lib/clickhouse/ \
-v $(realpath ./clickhouse/ch_logs):/var/log/clickhouse-server/ \
--name project-getntrends-test-clickhouse \
--ulimit nofile=262144:262144 \
clickhouse/clickhouse-server:22.2
