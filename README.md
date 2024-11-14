# Задание 1

## Скрин комманд

![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/run1.png)
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/run2.png)

## Пояснения

Для доступа к метрикам, необходимо было выдать доп. права.

Для этого использовались следующие манифесты:

kube-state-metrics-bind-role.yaml
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: kube-state-metrics-1-bind
subjects:
  - kind: ServiceAccount
    name: default
    namespace: kube-state-metrics
roleRef:
  kind: ClusterRole
  name: kube-state-metrics-1
  apiGroup: rbac.authorization.k8s.io
```

kube-state-metrics-claster-role.yaml
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: kube-state-metrics-1
rules:
  - apiGroups: ["*"]
    resources: ["*"]    
    verbs: ["get", "list", "watch"]
```

Изменить /etc/hosts:
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/hosts.png)

Открыть туннель:
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/tunnel.png)


## Метрики
По итогу запрос проходил:
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/curl.png)
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/kube_metrics.png)


# Задание 2

## Prometheus
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/prom-run.png)

## Метрики в Prometheus

При изучении метрик, наиболее интересными оказались следующие:

***kube_pod_container_resource_limits*** - количесество ресурсов, который заправшивает контейнер (видим, кто сколько "просит" cpu и memory)
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/metric1.png)

***kube_endpoint_address_available*** - количество доступных адресов в endpoint 
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/metric3.png)

***kube_node_role*** - роль ноды (видим, что роль control-plane, так как всего одна)
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/metric4.png)

***kube_ingress_created*** - timestamp создания Ingress (видим время в секундах создания ingress)
![Иллюстрация к проекту](https://github.com/randnull/sre-hw-6/blob/main/photo/metric2.png)





