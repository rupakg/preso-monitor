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

## Alerts Manager with Slack Integration

### Alerting

Alerting has been added to the stack with Slack integration. 2 Alerts have been added and are managed.

Alerts - `prometheus/alert.rules` Slack configuration - `alertmanager/config.yml`

The Slack configuration requires to build a custom integration.

* Open your slack team in your browser https://<your-slack-team>.slack.com/apps
* Create a new app
* Click build in the upper right corner
* Choose Incoming Web Hooks link under Send Messages
* Click on the "incoming webhook integration" link
* Select which channel
* Click on Add Incoming WebHooks integration
* Copy the Webhook URL into the alertmanager/config.yml URL section
* Fill in Slack username and channel

View Prometheus alerts `http://<Host IP Address>:9090/alerts` and view Alert Manager `http://<Host IP Address>:9093`

### Test Alerts

A quick test for your alerts is to stop a service. Stop the node_exporter container and you should notice shortly the alert arrive in Slack. Also check the alerts in both the Alert Manager and Prometheus Alerts just to understand how they flow through the system.

**High load test alert**

```
docker run --rm -it busybox sh -c "while true; do :; done"
```

Let this run for a few minutes and you will notice the load alert appear. Then Ctrl+C to stop this container.