<!-- llm-readme-management spec=1 commit=0f3f123c161c1932fec8fc07a7daa3096c6f4987 template=helm model=qwen3.6-35b-a3b digest=5b6cfbe96d9f generated=2026-09-08T21:43:39Z -->
<a href="https://hauke.cloud" target="_blank"><img src="https://img.shields.io/badge/home-hauke.cloud-brightgreen" alt="hauke.cloud" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud" target="_blank"><img src="https://img.shields.io/badge/github-hauke.cloud-blue" alt="hauke.cloud Github Organisation" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud/llm-readme-management" target="_blank"><img src="https://img.shields.io/badge/template-helm-orange" alt="Repository type - helm" style="display: block;" /></a>


# Matrix Hookshot


<img src="https://raw.githubusercontent.com/hauke-cloud/.github/main/resources/img/organisation-logo-small.png" alt="hauke.cloud logo" width="109" height="123" align="right">


<llm header hint="Name the chart and what it deploys.">

This Helm chart, `matrix-hookshot`, deploys a Matrix Hookshot instance onto Kubernetes, bridging a homeserver with external services like GitHub, GitLab, and Jira. It manages the Hookshot StatefulSet, configuration secrets, and an optional Redis dependency for encrypted rooms. You should keep reading if you are a Kubernetes operator or cluster administrator needing to relay external events into Matrix.

</llm>


## :book: Description

<llm description>

This repository provides a Helm chart that deploys Matrix Hookshot onto Kubernetes, enabling you to bridge your Matrix homeserver with external services like GitHub, GitLab, Jira, and Figma. It addresses the need to relay events from these platforms directly into Matrix rooms by packaging the `halfshot/matrix-hookshot` container as a StatefulSet. The chart handles the underlying infrastructure requirements, including optional Redis integration for end-to-end bridge encryption and automatic management of application configuration, registration tokens, and encryption keys.

As part of the `hauke-cloud` Helm repository, it is published as an OCI artifact to `ghcr.io/hauke-cloud/charts/matrix-hookshot` for straightforward cluster integration. The chart manages the following components:
- Deploys the Hookshot container alongside a conditional Redis sub-chart for encrypted room state storage.
- Renders and mounts configuration, registration, and passkey files into the application container.
- Exposes webhook, metrics/provisioning, and appservice ports through a single Kubernetes Service.
- Optionally provisions separate Ingress resources with TLS support for webhook and appservice traffic.

</llm>


## :clipboard: Requirements

<llm requirements hint="Give the Kubernetes version constraint from Chart.yaml, the Helm version, and any dependency charts or CRDs that must already be present.">

Before you deploy this chart, ensure your environment meets these requirements:
- Kubernetes cluster v1.14+ (v1.17+ required for HPA API support)
- Helm v3.x installed locally
- Access to `ghcr.io/hauke-cloud/charts` (OCI registry credentials or public read access)
- A running Matrix homeserver (Synapse or compatible) with appservice registration tokens (`as_token`, `hs_token`) and a configured domain/URL
- An Ingress controller matching your chosen `className` (required if enabling ingress)
- A storage provisioner matching the default `default` storage class (required if enabling encryption)
- The Bitnami Redis v23.1.6 sub-chart in your Helm repository cache

</llm>


## 🚀 Getting started

<llm getting_started hint="helm repo add, helm install and helm upgrade with the real repository URL and chart name. Show a values override only if the chart needs one to start.">

1. You clone the repository and enter the directory.
```bash
git clone https://github.com/hauke-cloud/matrix-hookshot.git
cd matrix-hookshot
```
2. You download the Redis

</llm>


## :airplane: Usage

<llm usage hint="Show installing with a values file, and how to reach or verify the deployed workload.">

Once you have a Kubernetes cluster and Helm 3 ready, you consume this chart directly from the OCI registry. You typically supply your Matrix homeserver details, appservice tokens, and encryption settings through a custom values file rather than inline flags.

To install the bridge with your configuration:
```bash
helm install matrix-hookshot oci://ghcr.io/hauke-cloud/charts/matrix-hookshot --version 0.1.0 -f my-values.yaml
```
Your `my-values.yaml` should populate `hookshot.config` with your homeserver domain and URLs, provide `hookshot.registration` tokens (`as_token`, `hs_token`), and set `hookshot.passkey`. If you need encrypted room state, enable the Redis sub-chart by setting `hookshot.encryption.enabled` to true and supply a `redisUri` in your config.

After deployment, verify the workload is running and reachable. The chart creates a StatefulSet named after your release and exposes ports 9000, 9001, and 9002 via a Service. You can check pod status with:
```bash
kubectl get pods -l app.kubernetes.io/name=matrix-hookshot
```
To confirm the webhook listener is accepting connections, you can run the built-in test-connection pod or curl the service directly:
```bash
kubectl run test-connection --rm -it --image=busybox -- wget -qO- http://matrix-hookshot-webhook:9000
```
If you configured `ingress.webhook.enabled` or `ingress.appservice.enabled`, you can also reach the bridge through your cluster's ingress controller at the specified hostnames.

</llm>


## :wrench: Configuration

<llm configuration hint="A table of the top-level values from values.yaml: key, default, description. Point at values.yaml for the full set.">

</llm>


## 📄 License

This Project is licensed under the GNU General Public License v3.0

- see the [LICENSE](LICENSE) file for details.


## :coffee: Contributing

To become a contributor, please check out the [CONTRIBUTING](CONTRIBUTING.md) file.


## :email: Contact

For any inquiries or support requests, please open an issue in this
repository or contact us at [contact@hauke.cloud](mailto:contact@hauke.cloud).
