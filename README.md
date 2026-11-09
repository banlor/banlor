# Mikhail Basov

### Senior DevOps Engineer at Sberbank

I have 5+ years in production infrastructure. In Sberbank's Risk Division I administer 24 Kubernetes clusters across all environments and run 70+ microservices in production and 6 LLM agents. I built the release platform and the unattended rollout service behind about 150 releases a week. I also built an AI code reviewer that handles 1,200+ pull requests a day at peak. Outside work I fix shipped Prometheus alert rules. My fixes are merged in Ceph, Rook, Grafana Mimir and other projects.

Astana, Kazakhstan · open to remote work and relocation · [LinkedIn](https://linkedin.com/in/michael-basov) · [michael.s.basov@gmail.com](mailto:michael.s.basov@gmail.com)

<sub>Also written as Michael Basov.</sub>

[![Merged upstream PRs](https://img.shields.io/github/issues-search?query=author%3Abanlor%20is%3Apr%20is%3Amerged%20-user%3Abanlor%20-user%3Aruslan-shaydullin&label=merged%20upstream%20PRs&style=flat-square)](https://github.com/search?q=author%3Abanlor+is%3Apr+is%3Amerged+-user%3Abanlor+-user%3Aruslan-shaydullin&type=pullrequests)

## Work

Sberbank · Risk Division · remote · since February 2024 · Senior DevOps Engineer since July 2026

- I built the rollout service that deploys about **150 releases a week** to production. It installs them at night and on weekends, in the bank's maintenance windows. It re-checks approvals before each step, and a failed wave stops the waves after it. After a crash it checks what really ran instead of retrying blindly. Across the division, 86% of production installs now start unattended.
- I built the release platform (Python, PostgreSQL, Helm), and I am its only maintainer. Nearly all releases of the division are created on it. It assembles each release from Jira tasks and Nexus builds, fills in the change request and moves it through quality gates. Release coordination went from **2–4 hours to under 10 minutes**. After my 2026 redesign the platform grew from 2 teams to about 40.
- I moved our services and their CI from OpenShift to Kubernetes. I write their Helm charts for Argo CD (GitOps), with Istio routing, retries and mTLS gateway rules as templates.
- I write CI/CD pipelines as code in Jenkins on Groovy shared libraries, with SAST/SCA scans and Vault secrets.
- I operate 70+ microservices in production with a 99.9% SLO. I resolve incidents and write root cause analyses, troubleshooting with Grafana, ELK and Dynatrace. I designed the Prometheus metrics and alerts for the services I built.
- I manage Kafka topics and ACLs for our services: about 250 topics on a 3-broker cluster.
- I initiated and shipped an AI code reviewer for Bitbucket pull requests: **1,200+ a day at peak**, 30 s median latency. It started as a Jenkins job. When the load grew, I rewrote it as a Python service on Kubernetes. It won the internal 2025 Engineering Achievement of the Year award. I presented it at an internal engineering conference.
- I operate 6 LLM agents in production. I also built a RAG assistant for credit managers: PostgreSQL with pgvector, a Confluence knowledge base and a second model that checks answers. In its pilot it closed 30% of routine requests with no human involved.

From 2022 to 2024 I was a Systems Engineer at USSC (Ural Security Systems Center) in Yekaterinburg. I deployed InfoWatch DLP and PAM for enterprise clients and ran a full DLP rollout on Linux. I also hardened Linux servers, administered PostgreSQL, troubleshot Docker and mentored 3 engineering interns. I started in IT in 2021 as a System Administrator at IT-Service: Windows Server, Active Directory, Bash and PowerShell.

## Merged upstream

I audit widely used Prometheus rule sets and send fixes upstream, usually with `promtool` regression tests. From May to November 2026, 17 of my PRs were merged in 10 projects. Twelve of them fix shipped alert rules.

My preprint *Silent or Wrong: Producer-Contract Defects in Shipped Prometheus Alerting Rules* comes out in November 2026. For the study I audited 1,808 shipped alert rules from 86 rule sets. I confirmed 31 distinct defects that `promtool` and offline Pint miss. In at least 19 of them the alert cannot fire in the situation it was written for.

| Project | PR | What changed | Status |
|---|---|---|---|
| [Ceph](https://github.com/ceph/ceph) | [#72067](https://github.com/ceph/ceph/pull/72067) | `CephPoolGrowthWarning` compared a fraction with `95` instead of `0.95`, so it could never fire | Merged · [tracker #80856](https://tracker.ceph.com/issues/80856) |
| [Rook](https://github.com/rook/rook) | [#18453](https://github.com/rook/rook/pull/18453) · [#18476](https://github.com/rook/rook/pull/18476) | Pool-growth and NVMe-oF CPU alerts compared 0–1 values with `95` and `80`, so they could never fire | In 5 releases: [v1.20.9](https://github.com/rook/rook/releases/tag/v1.20.9), v1.20.10, v1.21.0–v1.21.2 |
| [Grafana Mimir](https://github.com/grafana/mimir) | [#16725](https://github.com/grafana/mimir/pull/16725) · [#16739](https://github.com/grafana/mimir/pull/16739) | Ruler alerts ignored `server_error`, so real push and query failures stayed silent. A KEDA alert read a metric that KEDA 2.17 removed. It now reads the new metric and falls back to the old one | Merged · in [CHANGELOG](https://github.com/grafana/mimir/blob/main/CHANGELOG.md), unreleased |
| [Grafana jsonnet-libs](https://github.com/grafana/jsonnet-libs) | [#1709](https://github.com/grafana/jsonnet-libs/pull/1709) · [#1710](https://github.com/grafana/jsonnet-libs/pull/1710) · [#1716](https://github.com/grafana/jsonnet-libs/pull/1716) · [#1717](https://github.com/grafana/jsonnet-libs/pull/1717) · [#1718](https://github.com/grafana/jsonnet-libs/pull/1718) | Alerts in 9 mixins, including Istio, Jaeger and F5 BIG-IP, stayed silent or fired when values fell. Causes included 0–1 ratios compared with percent thresholds, `increase()` on gauges and broken vector matching | Merged |
| [awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) | [#646](https://github.com/samber/awesome-prometheus-alerts/pull/646) | Repaired 7 rules: a Kubernetes rule file that failed to load, missing series, unreachable thresholds. Added `promtool` tests to CI | Merged |
| [argo-cd-mixin](https://github.com/adinhodovic/argo-cd-mixin) | [#41](https://github.com/adinhodovic/argo-cd-mixin/pull/41) | Latency alerts required a P95 above the last histogram bucket, which is unreachable | Merged |
| [vLLM Production Stack](https://github.com/vllm-project/production-stack) | [#940](https://github.com/vllm-project/production-stack/pull/940) · [#943](https://github.com/vllm-project/production-stack/pull/943) | Added a per-model request latency histogram to the router. Fixed a dashboard that counted every backend once per router replica | Released in [vllm-stack 0.1.11](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.11) · [0.1.12](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.12) |

One example is [Mimir #16725](https://github.com/grafana/mimir/pull/16725). `MimirRulerTooManyFailedPushes` and `MimirRulerTooManyFailedQueries` counted only failures with `reason="error"` or no reason. But the ruler records server-side failures as `server_error`. So a ruler failing 5% of its queries would not page anyone. The selectors now include `server_error`, keep legacy series and exclude `client_error`. In synthetic checks the query alert now fires on 5% server errors mixed with 20% client errors. It stays quiet on client errors alone or on exactly 1% server errors.

Also merged: [VictoriaMetrics #11591](https://github.com/VictoriaMetrics/VictoriaMetrics/pull/11591) (Azure workload identity for `azure_sd_configs`, credited in the changelog) · [kubernetes/website #55710](https://github.com/kubernetes/website/pull/55710) (Russian translation of the docs page on Linux node security) · [opentelemetry-python-contrib #4539](https://github.com/open-telemetry/opentelemetry-python-contrib/pull/4539) (test-dependency update for google-genai)

Open alert-rule PRs: [etcd #22701](https://github.com/etcd-io/etcd/pull/22701) · [Ceph #72211](https://github.com/ceph/ceph/pull/72211) · [Thanos #9057](https://github.com/thanos-io/thanos/pull/9057) · [Thanos #9058](https://github.com/thanos-io/thanos/pull/9058) · [kube-prometheus #2901](https://github.com/prometheus-operator/kube-prometheus/pull/2901) · [Grafana Mimir #16730](https://github.com/grafana/mimir/pull/16730) · [postgres_exporter #1397](https://github.com/prometheus-community/postgres_exporter/pull/1397)

## How I use AI

Claude Code and Codex do most of the investigation and draft the patches and tests. I write the plan and review every diff before a PR goes upstream. All 12 alert-rule PRs say how AI was used. At work I added an MCP server to my rollout service. AI coding agents can use it to build and check install plans under the same rules as people. Only a person can cancel an install.

## Stack

[![Kubernetes, OpenShift, Docker, Jenkins, Git, Bitbucket, Ansible, Terraform, AWS, Linux, Bash, Python, PostgreSQL, Redis, Kafka, Prometheus, Grafana, Elasticsearch](https://skillicons.dev/icons?i=kubernetes,openshift,docker,jenkins,git,bitbucket,ansible,terraform,aws,linux,bash,python,postgresql,redis,kafka,prometheus,grafana,elasticsearch&perline=9)](#stack)

Helm · Argo CD (GitOps) · Istio · Groovy shared libraries · Vault · Nexus · Jira · SAST/SCA · promtool · Dynatrace · ELK · pgvector · RAG · MCP · vLLM Production Stack (OSS)

- Cloud and IaC: AWS, Terraform, Ansible
- Studying: BSc Software Engineering at Ural Federal University, part-time, expected 2027
- Languages: English B2, Russian native
- Community: judge at CSC Back-to-School Hackathon 2026 (Devpost); judging CSC Winter Sparkathon, Nov 30 – Dec 6, 2026
