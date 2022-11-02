# Observability-stack

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

## 要求

- Kubernetes 1.16+
- Helm 3+

## 集群内部署

### metrics 部署

```bash
$ cd kubeservice-stack/OpsCenter/metrics/
$ kubectl create ns monitoring

$ vim value.yaml #编辑环境配置

$ helm install metrics . --namespace monitoring  ## 部署

$ helm upgrade metrics . --namespace monitoring  ## 更新配置

$ helm uninstall metrics . --namespace monitoring  ## 卸载
```

### logging 部署

```bash
$ cd kubeservice-stack/OpsCenter/logging/

$ cd loki
$ vim value.yaml #编辑环境配置
$ helm install loki . --namespace monitoring  ## 部署
$ helm upgrade loki . --namespace monitoring  ## 更新配置
$ helm uninstall loki . --namespace monitoring  ## 卸载

$ cd promtail
$ vim value.yaml #编辑环境配置
$ helm install promtail . --namespace monitoring  ## 部署
$ helm upgrade promtail . --namespace monitoring  ## 更新配置
$ helm uninstall promtail . --namespace monitoring  ## 卸载
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

## 集群外部署

TODO