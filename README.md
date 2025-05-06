<!-- markdownlint-disable-next-line -->
# <img src="https://opentelemetry.io/img/logos/opentelemetry-logo-nav.png" alt="OTel logo" width="45"> OpenTelemetry Demo

[![Slack](https://img.shields.io/badge/slack-@cncf/otel/demo-brightgreen.svg?logo=slack)](https://cloud-native.slack.com/archives/C03B4CWV4DA)
[![Version](https://img.shields.io/github/v/release/open-telemetry/opentelemetry-demo?color=blueviolet)](https://github.com/open-telemetry/opentelemetry-demo/releases)
[![Commits](https://img.shields.io/github/commits-since/open-telemetry/opentelemetry-demo/latest?color=ff69b4&include_prereleases)](https://github.com/open-telemetry/opentelemetry-demo/graphs/commit-activity)
[![Downloads](https://img.shields.io/docker/pulls/otel/demo)](https://hub.docker.com/r/otel/demo)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg?color=red)](https://github.com/open-telemetry/opentelemetry-demo/blob/main/LICENSE)
[![Integration Tests](https://github.com/open-telemetry/opentelemetry-demo/actions/workflows/run-integration-tests.yml/badge.svg)](https://github.com/open-telemetry/opentelemetry-demo/actions/workflows/run-integration-tests.yml)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/opentelemetry-demo)](https://artifacthub.io/packages/helm/opentelemetry-helm/opentelemetry-demo)
[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/9247/badge)](https://www.bestpractices.dev/en/projects/9247)

## Welcome to the OpenTelemetry Astronomy Shop Demo

This repository contains the OpenTelemetry Astronomy Shop, a microservice-based
distributed system intended to illustrate the implementation of OpenTelemetry in
a near real-world environment.

Our goals are threefold:

- Provide a realistic example of a distributed system that can be used to
  demonstrate OpenTelemetry instrumentation and observability.
- Build a base for vendors, tooling authors, and others to extend and
  demonstrate their OpenTelemetry integrations.
- Create a living example for OpenTelemetry contributors to use for testing new
  versions of the API, SDK, and other components or enhancements.

We've already made [huge
progress](https://github.com/open-telemetry/opentelemetry-demo/blob/main/CHANGELOG.md),
and development is ongoing. We hope to represent the full feature set of
OpenTelemetry across its languages in the future.

If you'd like to help (**which we would love**), check out our [contributing
guidance](./CONTRIBUTING.md).

If you'd like to extend this demo or maintain a fork of it, read our
[fork guidance](https://opentelemetry.io/docs/demo/forking/).

## CNAE quickstart 

This version has the following changes:
---
Open the `.env` file.
Change the `IMAGE_VERSION` and `DEMO_VERSION` to something that does not exist, e.g. `cnae-latest`to make sure it is not pulling images from a image repository.

Search and replace in the `kubernetes/opentelemetry-demo.yaml` for `ghcr.io/open-telemetry/demo:2.0.2` and replace it with `ghcr.io/open-telemetry/demo:cnae-latest`.

> 2.0.2 was the IMAGE_VERSION before it was changed. If you are on a different version, you have to search for a different version.
---

Make sure images are build within Minikube:

```shell
eval "$(minikube -p minikube docker-env)"
```

Then build the images:
```shell
docker compose build
```

Check that the images are correctly tagged with 
```shell
docker image ls
```

It should look like this:
```
REPOSITORY                                TAG                           IMAGE ID       CREATED              SIZE
ghcr.io/open-telemetry/demo               cnae-latest-frontend-proxy    b3b149f4fb20   9 seconds ago        165MB
ghcr.io/open-telemetry/demo               cnae-latest-load-generator    545dc2164884   20 seconds ago       1.61GB
ghcr.io/open-telemetry/demo               cnae-latest-frontend          99bb68b6c2b2   About a minute ago   700MB
ghcr.io/open-telemetry/demo               cnae-latest-checkout          95ad43af5261   2 minutes ago        30.3MB
ghcr.io/open-telemetry/demo               cnae-latest-fraud-detection   a5b687ad4c8d   2 minutes ago        290MB
ghcr.io/open-telemetry/demo               cnae-latest-shipping          c22a2e7f6eec   2 minutes ago        119MB
ghcr.io/open-telemetry/demo               cnae-latest-currency          aa6e22c8a59f   2 minutes ago        107MB
ghcr.io/open-telemetry/demo               cnae-latest-ad                06d748afa9ed   2 minutes ago        387MB
ghcr.io/open-telemetry/demo               cnae-latest-flagd-ui          7619154a95d9   3 minutes ago        844MB
ghcr.io/open-telemetry/demo               cnae-latest-recommendation    7361653f3e1f   3 minutes ago        188MB
ghcr.io/open-telemetry/demo               cnae-latest-quote             929a2c0f9a45   3 minutes ago        539MB
ghcr.io/open-telemetry/demo               cnae-latest-cart              281f877eed02   4 minutes ago        117MB
ghcr.io/open-telemetry/demo               cnae-latest-accounting        b5889b83cce0   4 minutes ago        273MB
ghcr.io/open-telemetry/demo               cnae-latest-product-catalog   038d3f811157   4 minutes ago        27.6MB
ghcr.io/open-telemetry/demo               cnae-latest-email             72622de4e993   4 minutes ago        223MB
ghcr.io/open-telemetry/demo               cnae-latest-payment           444df0f888ff   5 minutes ago        204MB
ghcr.io/open-telemetry/demo               cnae-latest-image-provider    5d6312a457fc   6 minutes ago        222MB
ghcr.io/open-telemetry/demo               cnae-latest-kafka             4d0154e5b0ca   6 minutes ago        392MB
```


Then create the kubernetes deployment:

```shell
kubectl create -f kubernetes/opentelemetry-demo.yaml -n otel-demo
```

Open the Frontend via

```shell
minikube service frontend-proxy -n otel-demo
```

### Other remarks

Make sure to use 

```shell
kubectl create
```
instead of 
```shell
kubectl apply
```

Make sure to deploy it in the namespace `otel-demo` as some parts are hardcoded to it.

---
## Original Documentation below

You can be up and running with the demo in a few minutes. Check out the docs for
your preferred deployment method:

- [Docker](https://opentelemetry.io/docs/demo/docker_deployment/)
- [Kubernetes](https://opentelemetry.io/docs/demo/kubernetes_deployment/)

## Documentation

For detailed documentation, see [Demo Documentation][docs]. If you're curious
about a specific feature, the [docs landing page][docs] can point you in the
right direction.

## Demos featuring the Astronomy Shop

We welcome any vendor to fork the project to demonstrate their services and
adding a link below. The community is committed to maintaining the project and
keeping it up to date for you.

|                           |                |                                  |
|---------------------------|----------------|----------------------------------|
| [AlibabaCloud LogService] | [Google Cloud] |  [Oracle]                        |
| [AppDynamics]             | [Grafana Labs] |  [Sentry]                        |
| [Aspecto]                 | [Guance]       |  [ServiceNow Cloud Observability]|
| [Axiom]                   | [Honeycomb.io] |  [SigNoz]                        |
| [Axoflow]                 | [Instana]      |  [Splunk]                        |
| [Azure Data Explorer]     | [Kloudfuse]    |  [Sumo Logic]                    |
| [Coralogix]               | [Last9]        |  [TelemetryHub]                  |
| [Dash0]                   | [Liatrio]      |  [Teletrace]                     |
| [Datadog]                 | [Logz.io]      |  [Tracetest]                     |
| [Dynatrace]               | [New Relic]    |  [Uptrace]                       |
| [Elastic]                 | [OpenSearch]   |                                  |

## Contributing

To get involved with the project see our [CONTRIBUTING](CONTRIBUTING.md)
documentation. Our [SIG Calls](CONTRIBUTING.md#join-a-sig-call) are every other
Wednesday at 8:30 AM PST and anyone is welcome.

## Project leadership

[Maintainers](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#maintainer)
([@open-telemetry/demo-maintainers](https://github.com/orgs/open-telemetry/teams/demo-maintainers)):

- [Juliano Costa](https://github.com/julianocosta89), Datadog
- [Mikko Viitanen](https://github.com/mviitane), Dynatrace
- [Pierre Tessier](https://github.com/puckpuck), Honeycomb

[Approvers](https://github.com/open-telemetry/community/blob/main/guides/contributor/membership.md#approver)
([@open-telemetry/demo-approvers](https://github.com/orgs/open-telemetry/teams/demo-approvers)):

- [Cedric Ziel](https://github.com/cedricziel) Grafana Labs
- [Penghan Wang](https://github.com/wph95), AppDynamics
- [Reiley Yang](https://github.com/reyang), Microsoft
- [Roger Coll](https://github.com/rogercoll), Elastic
- [Ziqi Zhao](https://github.com/fatsheep9146), Alibaba

Emeritus:

- [Austin Parker](https://github.com/austinlparker)
- [Carter Socha](https://github.com/cartersocha)
- [Michael Maxwell](https://github.com/mic-max)
- [Morgan McLean](https://github.com/mtwo)

### Thanks to all the people who have contributed

[![contributors](https://contributors-img.web.app/image?repo=open-telemetry/opentelemetry-demo)](https://github.com/open-telemetry/opentelemetry-demo/graphs/contributors)

[docs]: https://opentelemetry.io/docs/demo/

<!-- Links for Demos featuring the Astronomy Shop section -->

[AlibabaCloud LogService]: https://github.com/aliyun-sls/opentelemetry-demo
[AppDynamics]: https://community.appdynamics.com/t5/Knowledge-Base/How-to-observe-OpenTelemetry-demo-app-in-Splunk-AppDynamics/ta-p/58584
[Aspecto]: https://github.com/aspecto-io/opentelemetry-demo
[Axiom]: https://play.axiom.co/axiom-play-qf1k/dashboards/otel.traces.otel-demo-traces
[Axoflow]: https://axoflow.com/opentelemetry-support-in-more-detail-in-axosyslog-and-syslog-ng/
[Azure Data Explorer]: https://github.com/Azure/Azure-kusto-opentelemetry-demo
[Coralogix]: https://coralogix.com/blog/configure-otel-demo-send-telemetry-data-coralogix
[Dash0]: https://github.com/dash0hq/opentelemetry-demo
[Datadog]: https://docs.datadoghq.com/opentelemetry/guide/otel_demo_to_datadog
[Dynatrace]: https://www.dynatrace.com/news/blog/opentelemetry-demo-application-with-dynatrace/
[Elastic]: https://github.com/elastic/opentelemetry-demo
[Google Cloud]: https://github.com/GoogleCloudPlatform/opentelemetry-demo
[Grafana Labs]: https://github.com/grafana/opentelemetry-demo
[Guance]: https://github.com/GuanceCloud/opentelemetry-demo
[Honeycomb.io]: https://github.com/honeycombio/opentelemetry-demo
[Instana]: https://github.com/instana/opentelemetry-demo
[Kloudfuse]: https://github.com/kloudfuse/opentelemetry-demo
[Last9]: https://last9.io/docs/integrations-opentelemetry-demo/
[Liatrio]: https://github.com/liatrio/opentelemetry-demo
[Logz.io]: https://logz.io/learn/how-to-run-opentelemetry-demo-with-logz-io/
[New Relic]: https://github.com/newrelic/opentelemetry-demo
[OpenSearch]: https://github.com/opensearch-project/opentelemetry-demo
[Oracle]: https://github.com/oracle-quickstart/oci-o11y-solutions/blob/main/knowledge-content/opentelemetry-demo
[Sentry]: https://github.com/getsentry/opentelemetry-demo
[ServiceNow Cloud Observability]: https://docs.lightstep.com/otel/quick-start-operator#send-data-from-the-opentelemetry-demo
[SigNoz]: https://signoz.io/blog/opentelemetry-demo/
[Splunk]: https://github.com/signalfx/opentelemetry-demo
[Sumo Logic]: https://www.sumologic.com/blog/common-opentelemetry-demo-application/
[TelemetryHub]: https://github.com/TelemetryHub/opentelemetry-demo/tree/telemetryhub-backend
[Teletrace]: https://github.com/teletrace/opentelemetry-demo
[Tracetest]: https://github.com/kubeshop/opentelemetry-demo
[Uptrace]: https://github.com/uptrace/uptrace/tree/master/example/opentelemetry-demo
