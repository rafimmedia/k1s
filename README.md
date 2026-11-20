# k1s

Watching Kubernetes resources from a terminal usually means rerunning `kubectl` commands and comparing output by hand. k1s keeps a selected resource view refreshed so you can observe cluster changes as they happen.

## Features

- Show Kubernetes resources for a selected namespace.
- Refresh the current resource list in real time.
- Accept resource type names, plural forms, singular forms, and short names supported by `kubectl`.
- Use the local kubeconfig and the same default cluster context as `kubectl`.

## Installation

k1s is a Bash script. Download it, make it executable, and place it in a directory on your `PATH`:

```bash
curl -LO https://raw.githubusercontent.com/weibeld/k1s/master/k1s
chmod +x k1s
sudo install -m 0755 k1s /usr/local/bin/k1s
```

On macOS, you can also install it with Homebrew:

```bash
brew install weibeld/tap/k1s
```

### Dependencies

Install these commands before running k1s:

- [`kubectl`](https://kubernetes.io/docs/tasks/tools/)
- [`jq`](https://jqlang.github.io/jq/)
- [`curl`](https://curl.se/)
- [`watch`](https://linux.die.net/man/1/watch)

For example, on Debian or Ubuntu:

```bash
sudo apt-get update
sudo apt-get install -y curl jq watch
```

Install `kubectl` by following the [official Kubernetes instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/). On macOS, Homebrew can install the command-line dependencies:

```bash
brew install jq watch curl kubernetes-cli
```

## Usage

k1s reads the kubeconfig used by `kubectl` on your machine. Run it with an optional namespace and resource type:

```bash
k1s default pods
```

The command syntax is:

```bash
k1s [<namespace>] [<resource-type>]
```

Defaults:

| Argument | Default |
|---|---|
| `<namespace>` | `default` |
| `<resource-type>` | `pods` |

Use `-` as the namespace to query all namespaces for namespaced resources, or no namespace for cluster-scoped resources. Resource types accepted by `kubectl api-resources` can be used, including short names such as `po`.

```bash
k1s - deployments
```

List available resource types with:

```bash
kubectl api-resources
```

Press `Ctrl-C` to exit.

## License

k1s is released under the [MIT License](https://opensource.org/licenses/MIT).

This project is based on [`weibeld/k1s`](https://github.com/weibeld/k1s), which is also released under the MIT License. Copyright and license notices from the original project are retained where applicable.

