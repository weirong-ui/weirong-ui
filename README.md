# Hi，我是 weirong-ui 👋

云原生 / Kubernetes 方向，主要用 Go。相信「把手弄脏」是学会一件事的最短路径——所以这个账号里的仓库，都是**真的在跑、真的踩过坑**的东西。

## 🔭 正在做：[KubeStasis](https://github.com/weirong-ui/kubestasis)（原名 KubeSentry）

基于 controller-runtime 的 Kubernetes Operator：**Prometheus 多信号弹性伸缩 + 分级故障自愈 + 准入控制**。不满足于 HPA「只伸缩、不自愈」，想做一个能让应用自己变强、自己疗伤的控制系统。

- ✅ **P0–P4 全部闭环**：`App` CRD → Deployment/Service 自动管理；弹性伸缩（真 Prometheus 打流验证 1→5→1）；分级自愈（CrashLoop → 摘除 → 自动回滚，真集群 + CI 双验证）；金丝雀错误率自动回滚
- ✅ **Admission Webhook**：禁 latest / 跨字段校验 / 默认值注入，自签证书方案不依赖 cert-manager；cosign keyless 镜像签名 + Kyverno 策略（CKS 证据链）
- ✅ **手写 mini-Informer**：ListWatch → DeltaFIFO → Store → WorkQueue，约 400 行泛型实现
- ✅ **AI 推理弹性**：队列深度 / TTFT / KV cache 占用率三信号，vLLM 开箱即用
- 🧪 **100 个单元测试用例**，CI 四道门：docs / build / e2e（kind 真集群三条链路）/ 多架构镜像
- 🗓 **进行中**：压测对比表（vs 原生 HPA）、envtest、Helm Chart

## 📖 学习笔记：[cloud-native-notes](https://github.com/weirong-ui/cloud-native-notes)

只记项目里真的用到 / 真的踩到的东西，不抄文档、不背八股。每篇格式固定：

```
机制是什么 → 源码/命令在哪 → 我怎么验证的 → 我踩过的坑
```

已沉淀：kube-scheduler 调度流程、Service 与 kube-proxy、Reconcile 幂等与 Finalizer 时序、伸缩决策引擎、controller-gen 的 10 个坑，以及 Pod/Service/etcd 三篇线上排查手册。

## 🛠 技术栈

![Go](https://img.shields.io/badge/Go-00ADD8?logo=go&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?logo=prometheus&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)

`controller-runtime` · `client-go` · `kubebuilder` · `PromQL` · `kustomize` · `cosign` · `Kyverno`

## 📫 联系我

- Email：2771986015@qq.com
- 系列技术文章发布在[掘金 @weirong](https://juejin.cn/user/1835559210983642)
