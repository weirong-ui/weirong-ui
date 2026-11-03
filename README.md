# Hi，我是 weirong-ui 👋

云原生 / Kubernetes 方向，主要用 Go。相信「把手弄脏」是学会一件事的最短路径——所以这个账号里的仓库，都是**真的在跑、真的踩过坑**的东西。

## 🔭 正在做：[KubeSentry](https://github.com/weirong-ui/kubesentry)

基于 controller-runtime 的 Kubernetes Operator：**Prometheus 多信号弹性伸缩 + 分级故障自愈**。不满足于 HPA「只伸缩、不自愈」，想做一个能让应用自己变强、自己疗伤的控制系统。

- ✅ **P0 已闭环**：`App` CRD → 自动管理 Deployment/Service，Status/Conditions/Events 真实回写，28 个单测用例
- 🚧 **进行中**：QPS / P99 / 错误率多信号伸缩的端到端验证（冷却窗口 + 迟滞抑震算法已落地）
- 🗓 **规划**：故障自愈引擎（CrashLoop/OOM/5xx 分级处置）、金丝雀观察自动回滚、Admission Webhook、手写 mini-Informer、Helm Chart

## 📖 学习笔记：[cloud-native-notes](https://github.com/weirong-ui/cloud-native-notes)

只记项目里真的用到 / 真的踩到的东西，不抄文档、不背八股。每篇格式固定：

```
机制是什么 → 源码/命令在哪 → 我怎么验证的 → 我踩过的坑
```

已沉淀：kube-scheduler 调度流程、Service 与 kube-proxy、Reconcile 幂等与 Finalizer 时序、伸缩决策引擎、controller-gen 的 8 个坑，以及 Pod/Service/etcd 三篇线上排查手册。

## 🛠 技术栈

![Go](https://img.shields.io/badge/Go-00ADD8?logo=go&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)

`controller-runtime` · `client-go` · `kubebuilder` · `PromQL` · `kustomize`

## 📫 联系我

- Email：2771986015@qq.com
- 系列技术文章发布在掘金（见 KubeSentry README）
