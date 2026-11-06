# Mikhail Basov

### DevOps Engineer at Sberbank

I build the release platform for Sberbank's Risk division (about 1,500 microservices). Around 150 releases a week now go to production at night on their own. Outside work I find Prometheus alerts that can never fire and fix them in open-source projects.

Open to remote work and relocation · [Website](https://mikhailbasov.github.io/) · [LinkedIn](https://linkedin.com/in/michael-basov) · [michael.s.basov@gmail.com](mailto:michael.s.basov@gmail.com)

<sub>Also written as Michael Basov.</sub>

[![Merged upstream PRs](https://img.shields.io/github/issues-search?query=author%3Abanlor%20is%3Apr%20is%3Amerged%20-user%3Abanlor%20-user%3Aruslan-shaydullin&label=merged%20upstream%20PRs&style=flat-square)](https://github.com/search?q=author%3Abanlor+is%3Apr+is%3Amerged+-user%3Abanlor+-user%3Aruslan-shaydullin&type=pullrequests)

## At Sberbank

**Risk Division** · DevOps Engineer · remote · at Sberbank since 2024

- **Autonomous deployments.** About **150 releases a week** go to production unattended, in night and weekend maintenance windows. The system plans each rollout and re-checks the gates before every step. Engineers have almost stopped staying late for releases, and deployment errors went down.
- **Release orchestration.** Built it and run it (Python, PostgreSQL, async workers). It connects CI with Jira, Nexus and quality gates; coordinating a release went from **2–4 hours to under 10 minutes**.
- **AI code review.** Started and shipped a production reviewer for Bitbucket pull requests: **up to 1,200+ a day**, about **30 s** per review at the median. It got the internal *Engineering Achievement of the Year 2025* award, and I gave a talk about it at an internal conference.
- **Kubernetes.** I work with 24 of the division's ~100 clusters, dev to production, and run **70+ production services and 6 LLM agents** under a **99.9% SLO**. Incident response, RCA, automated recovery and graceful degradation.
- **RAG assistant** for credit managers. In its pilot it closed **30%** of routine requests with no human involved.

Before that (2022–2024): systems engineer at USSC, Yekaterinburg. Enterprise DLP and PAM rollouts, Linux hardening, PostgreSQL, mentoring three engineering interns.

## Merged upstream

Most of these are alert rules that could never fire. I audit widely used Prometheus alert rules for silent or misfiring alerts and fix them upstream with `promtool` regression tests. AI-assisted, disclosed in each PR. The write-up, *Silent or Wrong: Producer-Contract Defects in Shipped Prometheus Alerting Rules*, comes out as a preprint in November 2026.

| Project | PR | What changed | Shipped |
|---|---|---|---|
| [Ceph](https://github.com/ceph/ceph) · 17k★ | [#72067](https://github.com/ceph/ceph/pull/72067) | `CephPoolGrowthWarning` compared a fraction with `95` instead of `0.95`, so it could never fire | Merged · [tracker #80856](https://tracker.ceph.com/issues/80856) |
| [Rook](https://github.com/rook/rook) · CNCF graduated · 13k★ | [#18453](https://github.com/rook/rook/pull/18453) · [#18476](https://github.com/rook/rook/pull/18476) | Pool-growth and NVMe-oF CPU alerts compared 0–1 values with `95` and `80`, so they never fired | [v1.20.9](https://github.com/rook/rook/releases/tag/v1.20.9) |
| [Grafana Mimir](https://github.com/grafana/mimir) · 5k★ | [#16725](https://github.com/grafana/mimir/pull/16725) | Ruler alerts ignored `server_error`, so real push and query failures stayed silent | [CHANGELOG](https://github.com/grafana/mimir/blob/main/CHANGELOG.md) |
| | [#16739](https://github.com/grafana/mimir/pull/16739) | KEDA alert read a metric removed in KEDA 2.17; now supports old and new | Merged |
| [awesome-prometheus-alerts](https://github.com/samber/awesome-prometheus-alerts) · 8k★ | [#646](https://github.com/samber/awesome-prometheus-alerts/pull/646) | 7 rules repaired: a Kubernetes rule file that failed to load, missing series, unreachable thresholds. Added `promtool` tests to CI | Merged |
| [argo-cd-mixin](https://github.com/adinhodovic/argo-cd-mixin) | [#41](https://github.com/adinhodovic/argo-cd-mixin/pull/41) | Latency alerts required a P95 above the last histogram bucket, which is unreachable | Merged |
| [vLLM Production Stack](https://github.com/vllm-project/production-stack) · 2.7k★ | [#940](https://github.com/vllm-project/production-stack/pull/940) | Added a per-model request latency histogram to the router | [vllm-stack 0.1.11](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.11) |
| | [#943](https://github.com/vllm-project/production-stack/pull/943) | Dashboard counted every backend once per router replica | [vllm-stack 0.1.12](https://github.com/vllm-project/production-stack/releases/tag/vllm-stack-0.1.12) |

**One example: [Mimir #16725](https://github.com/grafana/mimir/pull/16725).** `MimirRulerTooManyFailedPushes` and `MimirRulerTooManyFailedQueries` matched `reason="error"`, but the ruler records server-side failures as `server_error`. So a ruler failing 5% of its queries never paged anyone. The selectors now include `server_error`, keep legacy series and exclude `client_error`. Synthetic checks: 5% server errors mixed with 20% client errors now fires; client errors alone, or exactly 1% server errors, do not.

Also merged: Russian localization of the Linux security docs in [kubernetes/website #55710](https://github.com/kubernetes/website/pull/55710).

**In review:** [Thanos #9057](https://github.com/thanos-io/thanos/pull/9057) · [Thanos #9058](https://github.com/thanos-io/thanos/pull/9058) · [kube-prometheus #2901](https://github.com/prometheus-operator/kube-prometheus/pull/2901) · [kubernetes-mixin #1306](https://github.com/kubernetes-sigs/kubernetes-mixin/pull/1306) · [Ceph #72211](https://github.com/ceph/ceph/pull/72211) · [postgres_exporter #1397](https://github.com/prometheus-community/postgres_exporter/pull/1397)

## How I use AI

Claude Code and Codex do the legwork: investigation, patches, tests. I write the plan, review every diff and answer for what gets merged. The AI reviewer above is the production version of the same approach. Upstream PRs say how AI was used and follow each project's AI policy.

## Stack

[![Stack](https://skillicons.dev/icons?i=kubernetes,docker,linux,postgres,kafka,redis,jenkins,ansible,python,bash,prometheus,grafana,elasticsearch,bitbucket&perline=15)](#stack)

Helm · Groovy shared libraries · PromQL / promtool · OpenTelemetry · Dynatrace · ELK · pgvector · RAG · MCP · Qwen

- **Certification:** AWS Solutions Architect – Associate (in progress)
- **Studying:** BSc Software Engineering at Ural Federal University, part-time, graduating in 2027
- **Languages:** English B2, Russian native
- **Community:** judge at CSC Back-to-School Hackathon 2026 (Devpost, 115 submissions); judging CSC Winter Sparkathon, Nov 30 – Dec 6, 2026
