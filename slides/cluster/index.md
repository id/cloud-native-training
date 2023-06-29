# Kubernetes 集群

---

## 负载均衡

**介绍**

- 服务负载均衡：使用服务对象将请求分发到标签相同的Pod。默认使用轮询或基于IP的负载均衡策略。
- 外部负载均衡：与云服务商集成，通过负载均衡器将外部流量转发到集群中的服务。
- Ingress控制器：配置HTTP/HTTPS流量路由规则，集成不同负载均衡器，如Nginx、Traefik等。

---

## 负载均衡

**服务负载均衡**

![:scale 40%](https://raw.githubusercontent.com/jacky-xbb/pics/main/uPic/of3FQL.png)

- Kubernetes中的服务对象代表一组Pod，并提供稳定的虚拟IP（Cluster IP）作为访问入口。
- 内置的负载均衡器（如kube-proxy）将请求均衡地分发到服务关联的后端Pod。
- 可以使用不同的负载均衡策略，如轮询、会话保持或基于IP的负载均衡。
- 服务负载均衡适用于集群内部流量，对于外部流量可结合使用外部负载均衡器或Ingress控制器。

---

## 负载均衡

**外部负载均衡**

![:scale 40%](https://raw.githubusercontent.com/jacky-xbb/pics/main/uPic/YXYrOf.png)

许多云提供商（如 AWS、Azure、Google Cloud 等）都提供了托管的负载均衡服务。通过在云平台上配置和使用这些负载均衡器，可以将外部流量分发到 Kubernetes 集群中的 Service。

---

## 负载均衡

**Ingress控制器**

![:scale 40%](https://raw.githubusercontent.com/jacky-xbb/pics/main/uPic/rhdGwj.png)

它负责处理 Ingress 对象，并根据定义的规则将外部流量路由到集群内部的 Service。
- 路由和流量转发：Ingress 控制器基于 Ingress 规则来路由和转发外部流量。Ingress 规则定义了访问集群内服务的规则，可以根据域名、路径、TLS 加密等进行流量转发和策略配置。
- 外部负载均衡：Ingress 控制器通常与负载均衡器配合使用，将外部流量均衡地分发到后端的 Service 或 Pod。负载均衡器可以是云提供商的负载均衡服务或软件负载均衡器，具体取决于部署环境。
- TLS 加密和安全性：Ingress 控制器支持通过 TLS（Transport Layer Security）进行流量的加密和安全传输。可以配置 TLS 证书和密钥，以保护外部流量的隐私和安全性。
- 多协议支持：Ingress 控制器可以支持多种协议，如 HTTP、HTTPS、TCP 和 UDP。它能够根据 Ingress 规则中定义的协议类型来处理和转发相应的流量。

---

## 自动伸缩

- 垂直扩展（Vertical Pod Autoscaling，VPA）：可以根据容器内资源的使用情况，自动或者手动调整容器的 CPU 和内存请求量，以优化资源利用和性能。
- 水平扩展（Horizontal Pod Autoscaling，HPA）：可以根据指标（如 CPU 使用率、内存使用率）自动调整副本数，使得应用程序能够根据负载的变化进行弹性扩容和缩容。
- 自动扩展集群（Cluster Autoscaling）：可以根据集群中的资源需求自动扩展或缩减集群的节点数。

---

## 自动伸缩

**VPA vs HPA**

![:scale 40%](https://raw.githubusercontent.com/jacky-xbb/pics/main/uPic/PqZwOd.png)

HPA 用于调整应用程序的副本数，以满足负载需求，而 VPA 用于调整单个 Pod 的资源配置，以优化性能和资源利用率。它们也可以一起使用，以确保应用程序在水平和垂直方向上都具有适当的资源配置。

---

## 自动伸缩

**HPA 例子**

```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: hello-deploy
  namespace: hpa-test
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hello-deploy
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```

- minReplicas：最小副本数
- maxReplicas：最大副本数
- targetCPUUtilizationPercentage：目标 CPU 利用率百分比，当这个 deployment 超过这个百分比，HPA 会自动增加副本数以满足负载需求。反之减少副本数。

---

# 自动伸缩

**自动扩展集群**
