[![Self test](https://github.com/kubescape/generate-vex-action/actions/workflows/self-test.yml/badge.svg)](https://github.com/kubescape/generate-vex-action/actions/workflows/self-test.yml)
[![GitHub](https://img.shields.io/github/license/kubescape/generate-vex-action)](https://github.com/kubescape/generate-vex-action/blob/main/LICENSE)
[![Slack](https://img.shields.io/badge/slack-kubescape-blueviolet?logo=slack)](https://cloud-native.slack.com/archives/C04EY3ZF9GE)

# Generate VEX with Kubescape GitHub Action

This GitHub Action is designed to generate a VEX (Vulnerability Exploitability
eXchange) document using Kubescape. It does this by deploying a Helm chart to a
KinD cluster and running a test command, which should run your suite of tests
and thereby generate usage information for Kubescape. The Action will then
produce a VEX document based on the information collected and save it as an
artifact.

## Inputs

- `helm-chart-path`: (Required) The path to the Helm chart that you want to
  test.
- `install-timeout`: (Optional) The amount of time to wait for the Helm chart
  to install. If omitted, the timeout will be set to 300 seconds.
- `namespace`: (Optional) The namespace that the Helm chart should be deployed
  to. If omitted, the namespace will be set to `tests`.
- `ready-condition`: (Optional) A condition that the action should wait for
  before collecting VEX information.
- `test-command`: (Optional) The command that should be run to test the
  deployment. This should be a command that runs your suite of tests. If
  omitted, no tests will be run and the VEX document will likely be unreliable
  as there will be no real usage information.

## Usage

To use this action in your workflow, include it in your workflow file with the required inputs:

```yaml
- uses: kubescape/generate-vex-action
  with:
    helm-chart-path: './path/to/your/chart' # Ex. './charts/hello-world'
    install-timeout: '300s' # This is the default value
    namespace: 'tests' # This is the default value
    ready-condition: 'your-condition' # Optional. Ex. `kubectl wait --for=condition=ready pod -l app.kubernetes.io/name=hello-world --timeout=300s -n tests`
    test-command: 'your-test-command' # Optional. Ex. `./ci/test_integration.sh`
```

## Example

To see an example of this Action in use, check out the [self test](./.github/workflows/self-test.yml) workflow in this repository.

## Contributing

We welcome contributions to this project. If you want to get involved with the project, take a look at the [Contributing](./CONTRIBUTING.md) guide.
