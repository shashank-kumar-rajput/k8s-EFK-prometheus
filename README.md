# ELK Stack with Prometheus and Grafana on Kubernetes

## Overview

This guide provides instructions for setting up an ELK (Elasticsearch, Logstash, Kibana) stack with Prometheus and Grafana on Kubernetes. The setup includes monitoring with Node Exporter and Elasticsearch Exporter.

## Prerequisites

- **Minikube** installed on your local machine.
- **kubectl** configured to interact with your Kubernetes cluster.

## Setup Guide

### 1. Start Minikube

Start your Minikube cluster:

```bash
minikube start
```
### 2. Deploy Elasticsearch
Create a YAML file for Elasticsearch deployment and service (main.yaml).
Apply the configuration:
```bash
kubectl apply -f main.yaml
```
### 3. Deploy Kibana
Create a YAML file for Kibana deployment and service (kibana.yaml).
Apply the configuration:
```bash
kubectl apply -f kibana.yaml
```
### 4. Deploy Prometheus and Node Exporter
Create YAML files for Prometheus deployment and service, and Node Exporter (prometheus.yaml, node-exporter.yaml).
Apply the configurations:
```bash
kubectl apply -f prometheus.yaml
kubectl apply -f node-exporter.yaml
```
### 5. Deploy Grafana
Create a YAML file for Grafana deployment and service (grafana.yaml).
Apply the configuration:
```bash
kubectl apply -f grafana.yaml
```
### 6. Accessing the Services
Use the following URLs to access your services, replacing <minikube_ip> with your Minikube IP:
```bash
Elasticsearch: http://<minikube_ip>:32000
Kibana: http://<minikube_ip>:30151
Prometheus: http://<minikube_ip>:30539
Grafana: http://<minikube_ip>:30589
```
### 7. Create Elasticsearch and Prometheus Exporter Users
Create a user for the Prometheus Elasticsearch Exporter:

```bash
curl -u elastic:<password> -X POST "http://<minikube_ip>:32000/_security/user/prometheus_exporter" -H "Content-Type: application/json" -d '{
  "password" : "<password>",
  "roles" : [ "superuser" ],
  "full_name" : "Prometheus Exporter",
  "enabled": true
}'
```
### 8. Monitoring and Visualization
Prometheus: Access Prometheus to monitor your Kubernetes cluster and Elasticsearch metrics.
Grafana: Use Grafana for visualizing data from Prometheus and Elasticsearch.
###  9. Launching the Kubernetes Dashboard
Start the Kubernetes dashboard:


```bash
minikube dashboard
```
This command will open the Kubernetes dashboard in your browser.

## Conclusion
With these steps, you now have a fully functional ELK stack integrated with Prometheus and Grafana for monitoring and visualization in your Kubernetes cluster. If any issues arise, check the logs and ensure all components are correctly configured.
