# Monitoring for Docker containers

Use Prometheus and cAdvisor to monitor Docker containers, and configure rules in AlertMenager to send alert notifications to Slack.

## Prometheus

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

View Prometheus alerts `http://localhost:9090/alerts` and view Alert Manager `http://localhost:9093`

### Test Alerts on Slack

A quick test for your alerts is to stop a service. Stop any of the containers and you should notice shortly the alert arrive in Slack. 

To spike the cpu usage and trigger an alert, run: 

```
$ docker run --rm -it busybox sh -c "while true; do :; done"
```
CTRL+C to stop the rouge container.

## Using Docker Playground

To quickly deploy the stack using Play with Docker (PWD), click the **Try in PWD** button below.

[![Try in PWD](https://github.com/play-with-docker/stacks/raw/master/assets/images/button.png)](https://labs.play-with-docker.com/?stack=https://raw.githubusercontent.com/rupakg/preso-monitor/master/pwd-stack.yml)

