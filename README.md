### Senior DevOps / Platform Engineer · Sberbank · Astana, Kazakhstan (UTC+5)

I run Kubernetes platforms in regulated banking and build the automation around them: release orchestration, AI code review, LLM agents in production. AI-native — I ship daily with Claude Code, Codex and multi-agent workflows.

Open to remote work and relocation · [LinkedIn](https://linkedin.com/in/michael-basov) · [michael.s.basov@gmail.com](mailto:michael.s.basov@gmail.com)

## Work

**Sberbank, Risk Division** — Senior DevOps Engineer · remote · since 2024

- **Release Orchestration Platform.** Built it and own it (Django, PostgreSQL, async workers). It wires CI to Jira, Nexus and quality gates. **470 releases/month**; release coordination went from **2–4 hours to under 10 minutes**.
- **AI code reviewer.** Initiated and shipped a production review service for Bitbucket: **1,200+ MRs/day** at **~30 s** median latency. Internal *Engineering Achievement of the Year 2025*.
- **Platform.** **70+ production services and 6 LLM agents** on Kubernetes (Helm, Jenkins, Groovy shared libraries). Incident response, RCA, automated recovery and graceful degradation.
- **RAG assistant.** Qwen + PostgreSQL/pgvector for internal support. In the pilot it closed **30%** of routine requests with no human involved.

Before that: systems engineer at USSC, Yekaterinburg — enterprise DLP and PAM rollouts, Linux hardening, PostgreSQL, mentoring interns.

## Open source

I ran an AI-assisted audit of widely used Prometheus alert rules, looking for alerts that can never fire or fire on the wrong signal, and fixed them upstream with `promtool` regression tests.

| Project | PR | What was broken |
|---|---|---|
| [Ceph](https://github.com/ceph/ceph) · 17k★ | [#72067](https://github.com/ceph/ceph/pull/72067) | `CephPoolGrowthWarning` compared a fraction with `95` instead of `0.95`, so it could never fire |
| [Rook](https://github.com/rook/rook) · 13k★ | [#18453](https://github.com/rook/rook/pull/18453) | Same pool-growth threshold bug in the Helm chart rules |
| | [#18476](https://github.com/rook/rook/pull/18476) | `NVMeoFHighGatewayCPU` compared a 0–1 rate with `80`, so it never fired |
| [awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) · 8k★ | [#646](https://github.com/samber/awesome-prometheus-alerts/pull/646) | 7 rules repaired: a Kubernetes rule file that failed to load, missing series, unreachable thresholds. Added `promtool` tests to CI |
| [Grafana Mimir](https://github.com/grafana/mimir) · 5k★ | [#16725](https://github.com/grafana/mimir/pull/16725) | Ruler alerts ignored `server_error`, so real push and query failures stayed silent |
| | [#16739](https://github.com/grafana/mimir/pull/16739) | KEDA alert read a metric removed in KEDA 2.17; now supports old and new |
| [argo-cd-mixin](https://github.com/adinhodovic/argo-cd-mixin) | [#41](https://github.com/adinhodovic/argo-cd-mixin/pull/41) | Latency alerts required a P95 above the last histogram bucket, which is unreachable |
| [vLLM Production Stack](https://github.com/vllm-project/production-stack) · 2.7k★ | [#940](https://github.com/vllm-project/production-stack/pull/940) | Added a per-model request latency histogram to the router |
| | [#943](https://github.com/vllm-project/production-stack/pull/943) | Dashboard counted every backend once per router replica |
| [Kubernetes website](https://github.com/kubernetes/website) | [#55710](https://github.com/kubernetes/website/pull/55710) | Russian localization of the Linux security docs |
| [OpenTelemetry Python Contrib](https://github.com/open-telemetry/opentelemetry-python-contrib) | [#4539](https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4539) | google-genai test dependency bump |

<details>
<summary><b>30+ more in review</b> — Thanos, kube-prometheus, kubernetes-mixin, Grafana jsonnet-libs, Envoy Gateway, Argo Workflows, CoreDNS…</summary>

<br>

- **Thanos** — [#9057](https://github.com/thanos-io/thanos/pull/9057) Replicate and Receive latency alerts · [#9058](https://github.com/thanos-io/thanos/pull/9058) Query gRPC error ratio
- **kube-prometheus** — [#2901](https://github.com/prometheus-operator/kube-prometheus/pull/2901) keep the cluster name in Alertmanager alert descriptions
- **kubernetes-mixin** — [#1306](https://github.com/kubernetes-sigs/kubernetes-mixin/pull/1306) API termination ratio and pod startup latency metric
- **Grafana jsonnet-libs** — 9 PRs fixing alert math across 16 mixins (Kafka, Jaeger, Cassandra, Istio, Windows, Tomcat…)
- **Ceph** — [#72211](https://github.com/ceph/ceph/pull/72211) NVMe-oF gateway CPU in percent
- **Grafana Mimir** — [#16730](https://github.com/grafana/mimir/pull/16730) gossip-ring endpoint alerts for Helm release Services
- **postgres_exporter** — [#1397](https://github.com/prometheus-community/postgres_exporter/pull/1397) alert on maximum transaction age
- **Envoy Gateway** — [#10059](https://github.com/envoyproxy/gateway/pull/10059) honor listener routing type without `sectionName`
- **Argo Workflows** — [#17029](https://github.com/argoproj/argo-workflows/pull/17029) share event recorder resources across namespaces
- **CoreDNS** — [#8566](https://github.com/coredns/coredns/pull/8566) cache: share entries across DNSSEC DO modes
- **Distribution** — [#4959](https://github.com/distribution/distribution/pull/4959) keep manifest deletion retryable after tag cleanup errors
- **Dagster** — [#34212](https://github.com/dagster-io/dagster/pull/34212) stop waiting after terminal init container failures · [#34209](https://github.com/dagster-io/dagster/pull/34209) batch materialization reads
- **VictoriaMetrics** — [#11591](https://github.com/VictoriaMetrics/VictoriaMetrics/pull/11591) Azure discovery: workload identity and SDK auth
- **vLLM Production Stack** — [#951](https://github.com/vllm-project/production-stack/pull/951) routing decisions counter · [#1079](https://github.com/vllm-project/production-stack/pull/1079) operator resource requests and limits
- **OpenLLMetry** — [#4089](https://github.com/traceloop/openllmetry/pull/4089) DSPy instrumentation, plus LangChain fixes

[All my upstream PRs →](https://github.com/search?q=author%3Abanlor+is%3Apr+-user%3Abanlor&type=pullrequests&s=created&o=desc)

</details>

## How I work with AI

- **Spec-first agentic delivery.** A written plan, fresh implementer and reviewer sub-agents for each slice, then a whole-branch review and a full test run before merge.
- **Governed multi-agent system** for OSS and research work: parallel Codex workers in isolated worktrees, independent reviewer agents, approval gates, rate limits, an audit log and a kill switch.

## Community

- **Judge, CSC Back-to-School Hackathon 2026** (Devpost, 115 submissions). Scored all 8 finalists on a 5-criterion rubric after reviewing demos and source code.
- **Judge, CSC Winter Sparkathon**, Nov 30 – Dec 6, 2026.

## Stack

[![Stack](https://skillicons.dev/icons?i=kubernetes,docker,linux,postgres,kafka,redis,jenkins,ansible,python,bash,django,prometheus,grafana,elasticsearch,aws,terraform,bitbucket&perline=17)](#stack)

Helm · Groovy shared libraries · PromQL / promtool · OpenTelemetry · Dynatrace · ELK · pgvector · RAG · Qwen · Claude Code · Codex

**Now:** AWS Solutions Architect Associate, AWS CloudOps Engineer Associate and Terraform Associate in progress · BSc Software Engineering at Ural Federal University (2027) · English B2, Russian native
