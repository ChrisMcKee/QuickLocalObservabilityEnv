# Local Grafana Cloud (using vector)

You can boot up the local grafana cloud stack with the following command:

Spins up

* Grafana (Glue/Visualisation)
* Prometheus (Metrics)
* OpenTelemetry Collector (configured for grpc -> Exports to tempo [traces] + prometheus [metrics])
* Loki (Logging)
* Tempo (Traces)
* Vector.dev (Log Aggregation)

```bash
docker compose -p observability -f docker-compose-observability.yaml up -d
```

If you wish to run the dev tools also you can run the following command:

```bash
docker compose -p devtools -f docker-compose-devtools.yaml up -d
```

or run both at once using

```bash
docker compose -p observability -f docker-compose-observability.yaml up --remove-orphans --volumes -d && docker compose -p devtools -f docker-compose-dev-tools.yaml up -d --remove-orphans
```

Stopping the stack can be done with the following command (--volumes will delete the data too)

```bash
docker compose -p observability -f docker-compose-observability.yaml down --remove-orphans --volumes -d && docker compose -p devtools -f docker-compose-dev-tools.yaml down -d --remove-orphans --volumes
```

output

```shell
[+] Running 15/15
 ✔ Container local-dev-sqlserver      Removed                                                                                                                                                                                                                                                    0.9s
 ✔ Container local-dev-elasticsearch  Removed                                                                                                                                                                                                                                                    1.0s
 ✔ Container local-dev-redis          Removed                                                                                                                                                                                                                                                    0.7s
 ✔ Container local-dev-mongo          Removed                                                                                                                                                                                                                                                    0.7s
 ✔ Container local-dev-rabbitmq       Removed                                                                                                                                                                                                                                                   10.3s
 ✔ Volume tools_grafana_data          Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_alertmanager_data     Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_prometheus_data       Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_mongo-data            Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_tempo_data            Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_redis-data            Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_loki_data             Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_rmq-data              Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Volume tools_vector_data           Removed                                                                                                                                                                                                                                                    0.0s
 ✔ Network tools_default              Removed
```

You can selectively start parts of the stack as follows:

Starting the observability stack, and rabbitmq out of the dev tools stack:

```bash
docker compose -p observability -f docker-compose-observability.yaml up --remove-orphans -d && docker compose -p devtools -f docker-compose-dev-tools.yaml up -d rabbitmq --remove-orphans
```
