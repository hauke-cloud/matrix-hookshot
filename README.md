

<a href="https://hauke.cloud" target="_blank"><img src="https://img.shields.io/badge/home-hauke.cloud-brightgreen" alt="hauke.cloud" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud" target="_blank"><img src="https://img.shields.io/badge/github-hauke.cloud-blue" alt="hauke.cloud Github Organisation" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud/readme-management" target="_blank"><img src="https://img.shields.io/badge/template-helm-orange" alt="Repository type - helm" style="display: block;" /></a>


# matrix-hookshot


<img src="https://raw.githubusercontent.com/hauke-cloud/.github/main/resources/img/organisation-logo-small.png" alt="hauke.cloud logo" width="109" height="123" align="right">


A Matrix bot for connecting to external services like GitHub, GitLab, JIRA, and more.

(This is a fork of https://github.com/matrix-org/matrix-hookshot)

This chart offers you:
- Several services are supported out of the box.
- Webhooks let you connect all kinds of services, with the ability to write rich templates using JavaScript.
- No external database is required, instead using Matrix state as a persistent store.
- End-to-Bridge encryption allows bots to be used in encrypted Matrix rooms.
- Powerful widgets let you configure Hookshot from a room or the Element Extensions Store.





## 🚀 Getting started
To get started, you need to clone the repository. Follow the steps below:

### 1. Clone the repository

Use the following command to clone the repository:

```bash
git clone https://github.com/hauke-cloud/matrix-hookshot.git
```

### 2. Navigate to the repository directory

Once the repository is cloned, navigate to the directory:

```bash
cd matrix-hookshot
```

### 3. Check the content

```bash
ls -la
```

This will display all the files and directories in the cloned repository.



## :airplane: Usage
### Deploying the chart

Since we provide the chart in our public Github repository deploying it is
quite simple. You can run the following command to template and install the chart to your Kubernetes cluster:

#### Template the Helm chart

```bash
helm template oci://ghcr.io/hauke-cloud/charts/matrix-hookshot
```

#### Deploy the Helm chart

```bash
helm install matrix-hookshot oci://ghcr.io/hauke-cloud/charts/matrix-hookshot --version 1.0.0
```



## 📄 License

This Project is licensed under the GNU General Public License v3.0

- see the [LICENSE](LICENSE) file for details.


## :coffee: Contributing

To become a contributor, please check out the [CONTRIBUTING](CONTRIBUTING.md) file.


## :email: Contact

For any inquiries or support requests, please open an issue in this
repository or contact us at [contact@hauke.cloud](mailto:contact@hauke.cloud).

