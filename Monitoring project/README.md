Monitoring and Alerting with Prometheus, PagerDuty, Grafana, and Alertmanager.


![image](https://github.com/user-attachments/assets/399dd071-1086-48c8-8b14-29172a95f2cf) 

Prometheus - PagerDuty - Grafana - Alertmanager Integration
This repository demonstrates the integration of Prometheus for monitoring, Grafana for visualization, Alertmanager for alerting, and PagerDuty for incident management.


Introduction
This project provides a comprehensive setup for monitoring and alerting using Prometheus, Grafana, Alertmanager, and PagerDuty. These tools work together to provide a robust monitoring solution with visualization and alerting capabilities.


Repository Structure
The repository contains the following files and scripts:

1.node_exporter.sh: Script to set up Node Exporter.
2.prometheus-Config.sh: Script for configuring Prometheus.
3.prometheus.yml: Configuration file for Prometheus.
4.prometheus.service.sh: Script to set up Prometheus as a service.
5.start-prom.sh: Script to start Prometheus.
6.queries.sh: Script containing Prometheus queries.
7.grafana.sh: Script to set up Grafana.
8.alert_manager.yml: Configuration file for Alertmanager.
9.alert_rules.yml: Alert rules configuration file.
10.alertmanager.service.yml: Service configuration for Alertmanager.
11.commands.sh: Script containing useful commands.


Prometheus
Prometheus is an open-source systems monitoring and alerting toolkit. It collects and stores metrics as time series data, recording information with a timestamp.

Prometheus Configuration: The prometheus.yml file is the main configuration file for Prometheus, defining scrape targets and other settings.
Node Exporter: A Prometheus exporter for hardware and OS metrics exposed by *nix kernels, setup script is 1.node_exporter.sh.
Grafana
Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics no matter where they are stored.

Setup Script: The 7.grafana.sh script is used to set up Grafana.
Integration with Prometheus: Grafana connects to Prometheus to visualize the collected metrics.
Alertmanager
Alertmanager handles alerts sent by client applications such as Prometheus. It takes care of deduplicating, grouping, and routing them to the correct receiver integration such as email, PagerDuty, or Slack.

Configuration File: The 8.alert_manager.yml file defines how alerts are handled.
Alert Rules: The 9.alert_rules.yml file specifies the alerting rules for Prometheus.
PagerDuty
PagerDuty is an incident management platform that provides reliable notifications, automatic escalations, on-call scheduling, and other functionality to help teams detect and fix infrastructure problems quickly.

Integration with Alertmanager: Alerts from Prometheus are sent to Alertmanager, which then routes them to PagerDuty based on the configuration.



