# Michael Basov

### Senior DevOps / Platform Engineer · Sberbank · Astana, Kazakhstan (UTC+5)

5+ years in production infrastructure. I run Kubernetes platforms in regulated banking and build the automation around them: release orchestration, observability, AI code review, LLM services in production. Upstream fixes merged in Ceph, Rook, Grafana Mimir and vLLM.

Open to remote work and relocation · [Website](https://mikhailbasov.github.io/) · [LinkedIn](https://linkedin.com/in/michael-basov) · [michael.s.basov@gmail.com](mailto:michael.s.basov@gmail.com)

[![Merged upstream PRs](https://img.shields.io/github/issues-search?query=author%3Abanlor%20is%3Apr%20is%3Amerged%20-user%3Abanlor%20-user%3Aruslan-shaydullin&label=merged%20upstream%20PRs&style=flat-square)](https://github.com/search?q=author%3Abanlor+is%3Apr+is%3Amerged+-user%3Abanlor+-user%3Aruslan-shaydullin&type=pullrequests)

## Work

**Sberbank, Risk Division** — Senior DevOps Engineer · remote · since 2024

- **Release Orchestration Platform.** Built it and own it (Django, PostgreSQL, async workers). It wires CI to Jira, Nexus and quality gates. **470 releases/month**; release coordination went from **2–4 hours to under 10 minutes**.
- **AI code reviewer.** Initiated and shipped a production review service for Bitbucket: **1,200+ MRs/day** at **~30 s** median latency. Internal *Engineering Achievement of the Year 2025*.
- **Platform.** **70+ production services and 6 LLM agents** on Kubernetes (Helm, Jenkins, Groovy shared libraries). Incident response, RCA, automated recovery and graceful degradation.
- **RAG assistant.** Qwen + PostgreSQL/pgvector for internal support. In the pilot it closed **30%** of routine requests with no human involved.

Before that (2022–2024): systems engineer at USSC, Yekaterinburg — enterprise DLP and PAM rollouts, Linux hardening, PostgreSQL, mentoring interns.

## Merged upstream

I audited widely used Prometheus alert rules for alerts that can never fire or fire on the wrong signal, and fixed them upstream with `promtool` regression tests. AI-assisted, disclosed in each PR.

| Project | PR | What was broken | Shipped |
|---|---|---|---|
| [Ceph](https://github.com/ceph/ceph) · 17k★ | [#72067](https://github.com/ceph/ceph/pull/72067) | `CephPoolGrowthWarning` compared a fraction with `95` instead of `0.95`, so it could never fire | Merged · [tracker #80856](https://tracker.ceph.com/issues/80856) |
| [Rook](https://github.com/rook/rook) · CNCF graduated · 13k★ | [#18453](https://github.com/rook/rook/pull/18453) · [#18476](https://github.com/rook/rook/pull/18476) | Pool-growth and NVMe-oF CPU alerts compared 0–1 values with `95` and `80`, so they never fired | [v1.20.9](https://github.com/rook/rook/releases/tag/v1.20.9) |
| [Grafana Mimir](https://github.com/grafana/mimir) · 5k★ | [#16725](https://github.com/grafana/mimir/pull/16725) | Ruler alerts ignored `server_error`, so real push and query failures stayed silent | [CHANGELOG](https://github.com/grafana/mimir/blob/main/CHANGELOG.md) |
| | [#16739](https://github.com/grafana/mimir/pull/16739) | KEDA alert read a metric removed in KEDA 2.17; now supports old and new | Merged |
| [awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) · 8k★ | [#646](https://github.com/samber/awesome-prometheus-alerts/pull/646) | 7 rules repaired: a Kubernetes rule file that failed to load, missing series, unreachable thresholds. Added `promtool` tests to CI | Merged |
| [argo-cd-mixin](https://github.com/adinhodovic/argo-cd-mixin) | [#41](https://github.com/adinhodovic/argo-cd-mixin/pull/41) | Latency alerts required a P95 above the last histogram bucket, which is unreachable | Merged |
| [vLLM Production Stack](https://github.com/vllm-project/production-stack) · 2.7k★ | [#940](https://github.com/vllm-project/production-stack/pull/940) | Added a per-model request latency histogram to the router | [vllm-stack 0.1.11](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.11) |
| | [#943](https://github.com/vllm-project/production-stack/pull/943) | Dashboard counted every backend once per router replica | [vllm-stack 0.1.12](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.12) |

**Closer look — [Mimir #16725](https://github.com/grafana/mimir/pull/16725).** `MimirRulerTooManyFailedPushes` and `MimirRulerTooManyFailedQueries` matched `reason="error"`, but the ruler records server-side failures as `server_error`, so a ruler failing 5% of its queries never paged. The selectors now include `server_error`, keep legacy series and exclude `client_error`. Synthetic checks: 5% server errors mixed with 20% client errors now fires; client errors alone, or exactly 1% server errors, do not.

Also merged: Russian localization of the Linux security docs in [kubernetes/website #55710](https://github.com/kubernetes/website/pull/55710).

**In review, same audit:** [Thanos #9057](https://github.com/thanos-io/thanos/pull/9057) · [Thanos #9058](https://github.com/thanos-io/thanos/pull/9058) · [kube-prometheus #2901](https://github.com/prometheus-operator/kube-prometheus/pull/2901) · [kubernetes-mixin #1306](https://github.com/kubernetes-sigs/kubernetes-mixin/pull/1306) · [Ceph #72211](https://github.com/ceph/ceph/pull/72211) · [postgres_exporter #1397](https://github.com/prometheus-community/postgres_exporter/pull/1397)

## How I use AI

Claude Code and Codex for investigation, patches and tests, with a written plan and a separate review pass before merge. The AI code reviewer above is the production version of that. Upstream PRs say how AI was used and follow each project's AI policy.

## Stack

[![Stack](https://skillicons.dev/icons?i=kubernetes,docker,linux,postgres,kafka,redis,jenkins,ansible,python,bash,django,prometheus,grafana,elasticsearch,bitbucket&perline=15)](#stack)

Helm · Groovy shared libraries · PromQL / promtool · OpenTelemetry · Dynatrace · ELK · pgvector · RAG · Qwen

**Now:** AWS Solutions Architect Associate, AWS CloudOps Engineer Associate and Terraform Associate in progress · BSc Software Engineering at Ural Federal University (2027) · English B2, Russian native

**Community:** judge, CSC Back-to-School Hackathon 2026 (Devpost, 115 submissions) · judge (upcoming), CSC Winter Sparkathon, Nov 30 – Dec 6, 2026
