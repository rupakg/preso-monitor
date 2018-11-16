# Monitoring for Docker containers

## Setting up Prometheus

* Prometheus Dashboard at `http://localhost:9090`
* Look at the targets are `http://localhost:9090/targets`
* Look at the metrics: `http://localhost:9090/metrics`
  * Add graph for following metrics:
  * `prometheus_http_response_size_bytes_sum`
  * `prometheus_http_request_duration_seconds_sum`

## Node Health

Add Node Exporter configuration to `docker-compose.yml` and `prometheus.yml`.

All containers need to use the same overlay network so that they can communicate with each other.

## cAdvisor

Add cAdvisor to `docker-compose.yml` and `prometheus.yml`.