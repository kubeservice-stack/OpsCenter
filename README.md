# Observability-stack

[![Lint and Test Charts](https://github.com/kubeservice-stack/OpsCenter/actions/workflows/lint.yml/badge.svg)](https://github.com/kubeservice-stack/OpsCenter/actions/workflows/lint.yml)
[![Releases downloads](https://img.shields.io/github/downloads/kubeservice-stack/OpsCenter/total.svg)](https://github.com/kubeservice-stack/OpsCenter/releases)

Observability Stack 是基于云原生组件构建的OpsCenter系统。 包括 

> 基于`Prometheus`的`metrics`监控和报警

> 基于`Loki`的异构`logging` 监控、报警 和 搜索

> 基于`Tempo`的 `tracing` 的计算、报警 和 查询 


## 设计技术

1. [kube-prometheus stack](https://github.com/prometheus-operator/kube-prometheus)
2. [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator)
3. [Grafana](http://grafana.com/) 
4. [Loki](https://github.com/grafana/loki)
5. [Promtail](https://grafana.com/docs/loki/latest/clients/promtail/)
6. [Tempo](https://github.com/grafana/tempo)
7. [Opentelemetry](https://opentelemetry.io/)

## 设计文档

整体设计文档： [https://kubeservice.cn/2022/11/07/devops-k8s-observability-stack/](https://kubeservice.cn/2022/11/07/devops-k8s-observability-stack/)

监控体系设计： 

- Pingmesh: [https://kubeservice.cn/2022/10/21/devops-k8s-pingmesh/](https://kubeservice.cn/2022/10/21/devops-k8s-pingmesh/)
- Monitoring: [https://kubeservice.cn/2022/10/20/devops-k8s-prometheus/](https://kubeservice.cn/2022/10/20/devops-k8s-prometheus/)

日志体系设计：

- kube-event: 
- Loki：[https://kubeservice.cn/2022/11/02/devops-k8s-logging/](https://kubeservice.cn/2022/11/02/devops-k8s-logging/)

调用链设计：

- Open Telemetry: 

## 要求

- Kubernetes 1.16+
- Helm 3+

## 其他条件

- kubelet、apiserver、scheduler 和 controller manager 开启metrics

## 集群内部署

### metrics 部署

```bash
$ cd kubeservice-stack/OpsCenter/metrics/
$ kubectl create ns monitoring

$ kubectl apply -f ./metrics/crds/ .
$ vim value.yaml #编辑环境配置

$ helm install metrics . --namespace monitoring  ## 部署

$ helm upgrade metrics . --namespace monitoring  ## 更新配置

$ helm uninstall metrics --namespace monitoring  ## 卸载
```

或者 通过 `helm template` 方式部署

```bash
$ helm template metrics . --namespace monitoring > metrics-allinone.yaml
$ kubectl apply -f metrics-allinone.yaml
```

### logging 部署

```bash
$ cd kubeservice-stack/OpsCenter/logging/

$ cd loki
$ vim value.yaml #编辑环境配置
$ helm install loki . --namespace monitoring  ## 部署
$ helm upgrade loki . --namespace monitoring  ## 更新配置
$ helm uninstall loki --namespace monitoring  ## 卸载

$ cd promtail
$ vim value.yaml #编辑环境配置
$ helm install promtail . --namespace monitoring  ## 部署
$ helm upgrade promtail . --namespace monitoring  ## 更新配置
$ helm uninstall promtail --namespace monitoring  ## 卸载
```

或者 通过 `helm template` 方式部署

```bash
$ helm template loki . --namespace monitoring > loki-allinone.yaml
$ kubectl apply -f loki-allinone.yaml

$ helm template promtail . --namespace monitoring > promtail-allinone.yaml
$ kubectl apply -f promtail-allinone.yaml
```

### tracing 部署

```bash
$ cd kubeservice-stack/OpsCenter/tracing/

$ cd tempo
$ vim value.yaml #编辑环境配置
$ helm install tempo . --namespace monitoring  ## 部署
$ helm upgrade tempo . --namespace monitoring  ## 更新配置
$ helm uninstall tempo . --namespace monitoring  ## 卸载
```


或者 通过 `helm template` 方式部署

```bash
$ helm template tempo . --namespace monitoring > tempo-allinone.yaml
$ kubectl apply -f tempo-allinone.yaml
```

## 集群外部署

TODO

## 效果演示

![Opscenter Demo](https://www.kubeservice.cn/img/devops/opscenter.gif)

