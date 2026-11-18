# Hi，我是 weirong-ui 👋

云原生 / Kubernetes 方向，主要用 Go。相信「把手弄脏」是学会一件事的最短路径——所以这个账号里的仓库，都是**真的在跑、真的踩过坑**的东西。

## 🔭 正在做：[KubeStasis](https://github.com/weirong-ui/kubestasis)（原名 KubeSentry）

基于 controller-runtime 的 Kubernetes Operator：**Prometheus 多信号弹性伸缩 + 分级故障自愈 + 准入控制**。不满足于 HPA「只伸缩、不自愈」，想做一个能让应用自己变强、自己疗伤的控制系统。定位是实现研究、**不打算被生产采用**：每条能力都附可复算的实测证据与失败记录，没实测的就标"未实测"。

- ✅ **P0–P4 全部闭环**：`App` CRD → Deployment/Service 自动管理；弹性伸缩（真 Prometheus 打流验证 1→5→1）；分级自愈（CrashLoop → 摘除 → 自动回滚，真集群 + CI 双验证）；金丝雀错误率自动回滚
- ✅ **Admission Webhook**：禁 latest / 跨字段校验 / 默认值注入，自签证书方案不依赖 cert-manager；cosign keyless 镜像签名 + Kyverno 策略（按 CKS 考点组织的安全实践）
- ✅ **手写 mini-Informer**：ListWatch → DeltaFIFO → Store → WorkQueue，约 400 行泛型实现
- ✅ **AI 推理弹性**：队列深度 / TTFT / KV cache 占用率三信号，默认 vLLM 指标名（`WithQuery` 可换 SGLang/TGI）——⚠️ 只有单测覆盖，**没在真实 vLLM 集群跑过**
- ✅ **envtest + Helm Chart**：真实 apiserver 的控制循环回归（创建、状态回写、删除放闸、漂移拉回四类链路）；chart 在真集群 `helm upgrade --install` 验证，自签 / cert-manager 双证书方案
- ✅ **压测对比 vs 原生 HPA**：同镜像、同资源、同流量时间线；前四轮废数据逐轮记了废因，其中一轮连原始 CSV 都没留，报告里如实标"未归档"。扩容响应的方差尚未补齐、只作定性参考——重复实验的判定线已预注册。**具体数字一律以仓库报告为准，这里不复述**
- 🧪 **单元测试 + CI 门**：docs / build（含 `-race` 数据竞争检测）/ envtest / chart / e2e（kind 真集群）/ 多架构镜像。用例数与最新状态只在[仓库 README](https://github.com/weirong-ui/kubestasis) 维护，这里不写数字（写一次就要同步一次，必然漂）

## 📖 学习笔记：[cloud-native-notes](https://github.com/weirong-ui/cloud-native-notes)

只记项目里真的用到 / 真的踩到的东西。每篇格式固定：

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

## 📜 认证

- **CKA** Certified Kubernetes Administrator · The Linux Foundation · 2026.11 · [verify credential](https://www.credly.com/badges/7075ca76-78a9-47b1-84dc-ea59c0f99d96/public_url)


## 📫 联系我

- 跑不通、发现文档写错：[开 Issue](https://github.com/weirong-ui/kubestasis/issues/new/choose)，有模板，附 `kubectl get events` 就够
- 设计、选型、或者想拿它练手：[Discussions](https://github.com/weirong-ui/kubestasis/discussions)
- 系列技术文章：[掘金 @weirong](https://juejin.cn/user/1835559210983642/posts)

## 开发方式说明

这个项目大量用 AI 辅助。按模块说清楚用在哪，"部分工作由 AI 协助"那种句子读不出信息，等于免责声明。

| 模块 | 分工 |
|---|---|
| `internal/controller`（Reconcile、status 回写、Finalizer 时序） | 骨架我写；冲突重试、删除放闸、条件竞态这些边界由 AI 起草，我逐行改 |
| `internal/scaler` / `internal/healer` | 语义我定：取最紧急者、迟滞只挡缩容、窗口状态放 status、`BelowTarget` 三态、分级顺序；实现与单测 AI 起草，我改 |
| `internal/webhook` | AI 起草；校验规则与默认值我定 |
| `pkg/miniinformer`（约 400 行泛型 ListWatch/DeltaFIFO/WorkQueue） | 我写；AI 用来对照 client-go 源码讲解 |
| `test/envtest`、`test/e2e` | 断言我定；样板 AI 起草 |
| `hack/`（报告复算、方差预检、文档一致性门） | AI 起草，口径我复核 |
| `docs/`、掘金文章 | 我写；AI 润色，数字与结论我回原始 CSV 核 |

一条底线：AI 写下的每个"已验证"都要有对应的命令输出，没有就删。STATUS 里那些"未实测"就是这条底线的产物。

可核验的痕迹：提交历史是多轮修复与重构（而非一次性导入）、5 轮压测含废轮及废因、
`hack/variance_precheck.py` 可对现有 CSV 独立重跑、重复实验的判定线在数据落盘前已预注册锁定。
`docs/STATUS.md` 明列「已知不解决的问题」。

上游 PR [#58555](https://github.com/kubernetes/website/pull/58555) 的讨论区里，我就 AI 辅助使用做过公开说明并附开 PR 前的人工核对记录。对某段实现或某条数据有疑问，直接开 issue 就行。

