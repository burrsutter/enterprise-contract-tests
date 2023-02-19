Grab CLI

```
cd ~/projects

git clone https://github.com/hacbs-contract/ec-cli.git

cd ec-cli

make build
```


```
export PATH=/Users/burr/projects/ec-cli/dist:$PATH
```

Test CLI

```
ec
```

```
Enterprise Contract CLI

Set of commands to help validate resources with the Enterprise Contract.

Usage:
  ec [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  create-pr   Create a GitHub pull request based on source and target branches
  fetch       Fetch policies and authorization data
  help        Help about any command
  inspect     Inspect policy rules
  replace     Replace image references in a given source
  track       Record resource references for tracking purposes
  validate    Validate conformance with the Enterprise Contract
  version     Print version information

Flags:
      --debug               same as verbose but also show function names and line numbers
  -h, --help                help for ec
      --kubeconfig string   path to the Kubernetes config file to use
      --quiet               less verbose output
      --verbose             more verbose output

Use "ec [command] --help" for more information about a command.
```


Add Policy and Integration Test

```
oc apply -f ec-policy.yaml

oc apply -f ec-integrationtest.yaml
```


```
open https://console.dev.redhat.com/hac/stonesoup
```

And add the following URL argument and reload page

https://console.dev.redhat.com/hac/stonesoup?mvp=false

Create Application 

Load in the following repository

https://github.com/burrsutter/ec-node-hello


Screenshots

https://www.screencast.com/t/UcI6QQEJhW5G

https://www.screencast.com/t/EVRIny0g


Extract container image info from Component

```
CONTAINERIMAGE=$(oc get component ec-node-hello-d4m7 -oyaml | yq .spec.containerImage)
echo $CONTAINERIMAGE
```

```
ec validate image --image $CONTAINERIMAGE
```

```
ec validate image --image $CONTAINERIMAGE --policy '{"configuration":null,"description":"ACME \u0026 co policy","publicKey":"-----BEGIN PUBLIC KEY-----\nMFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEODgxyIz09vBqJlXXzjp/X2h17WIt\njCVQhnDYVWHvXhw6rgqGeg6NTUxIEhRQqQZaF9mcBotHkuYGJfYZbai+FA==\n-----END PUBLIC KEY-----","sources":[{"data":["github.com/hacbs-contract/ec-policies//data"],"name":"EC Policies","policy":["github.com/hacbs-contract/ec-policies//policy/lib","github.com/hacbs-contract/ec-policies//policy/release"]}]}' --output yaml
```