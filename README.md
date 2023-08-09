# cloud-native-training

研发培训之云原生课程是一系列关于容器技术和 Kubernetes 的讲座，希望能帮助大家了解和应用容器化技术，构建可靠、可扩展的应用程序环境，并掌握在 Kubernetes 集群中部署和管理应用程序的最佳实践。

## 目录

### [容器的基本概念](https://emqx.github.io/cloud-native-training/slides/docker)
容器的基本概念，包含容器技术的概念、优点及基本操作等内容。

### [在 Kubernetes 上部署无状态应用](https://emqx.github.io/cloud-native-training/slides/deployment)
介绍 Kubernetes 的基本组件，从 Pod 的概念到 Serveice 的作用以及使用场景，最后通过 Deployment 部署应用并且进行滚动更新。

### [在 Kubernetes 上部署有状态应用](https://emqx.github.io/cloud-native-training/slides/statefulset)
介绍 Kubernetes 的有状态应用 StatefulSet，包括使用场景，与之相关的持久化卷, Headless Service，最后通过 StatefulSet 部署一个 EMQX 集群。

### [Kubernetes 集群](https://emqx.github.io/cloud-native-training/slides/cluster)
介绍 Kubernetes 的集群，包括集群负载均衡、自动伸缩、调度方式、高可用架构和安全管理的知识。

## 生成 PDF

```shell
decktape remark index.html ${name}.pdf

```




