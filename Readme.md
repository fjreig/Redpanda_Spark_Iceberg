
```
rpk profile create docker-compose-iceberg --set=admin_api.addresses=localhost:19644 --set=brokers=localhost:19092 --set=schema_registry.addresses=localhost:18081
```

```
rpk topic create key_value --topic-config=redpanda.iceberg.mode=key_value
rpk topic create value_schema_id_prefix --topic-config=redpanda.iceberg.mode=value_schema_id_prefix
```

```
echo "hello world" | rpk topic produce key_value --format='%k %v\n'
```

```
docker cp schema.avsc redpanda-0:schema.avsc
```

```
rpk registry schema create value_schema_id_prefix-value --schema schema.avsc
```

```
echo '{"user_id":2324,"event_type":"BUTTON_CLICK","ts":"2024-11-25T20:23:59.380Z"}\n{"user_id":3333,"event_type":"SCROLL","ts":"2024-11-25T20:24:14.774Z"}\n{"user_id":7272,"event_type":"BUTTON_CLICK","ts":"2024-11-25T20:24:34.552Z"}' | rpk topic produce value_schema_id_prefix --format='%v\n' --schema-id=topic
```

```
docker exec -it spark-iceberg python3 consulta.py
```

https://github.com/redpanda-data/redpanda-labs/tree/main/docker-compose/iceberg

https://www.tabular.io/apache-iceberg-cookbook/pyiceberg-get-started-api/