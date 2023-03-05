## EC CLI Tests

Possible Images

https://quay.io/repository/redhat-appstudio/user-workload?tab=tags

```
ec version
```

```
Version                     v0.1.962-253c2c0
Source ID                   253c2c0d73529f9b6a4bfb2f00c682bb129c5771
Change date                 2023-02-23 22:39:47 +0000 UTC (22 hours ago)
ECC                         v0.0.0-20221220151524-ad0f637efacf
OPA                         v0.49.1
Conftest                    v0.39.1
Red Hat AppStudio (shared)  v0.0.0-20220615221006-a71c1aa4b97f
Cosign                      v1.13.1
Sigstore                    v1.5.2
Rekor                       v0.12.1-0.20220915152154-4bb6f441c1b2
Tekton Pipeline             v0.42.0
Kubernetes Client           v0.26.1
```

How to find the pub key

```
oc -n tekton-chains get secret public-key -o json | jq '.data."cosign.pub" | @base64d' -r > cosign.pub
```

Convert Policy Yaml to JSON

```
ECPOLICY=$(kubectl create --dry-run=client -o jsonpath='{.spec}' -f ec-policy.yaml)
```

Container Image

```
CONTAINERIMAGE=${IMAGE:-"quay.io/redhat-appstudio/user-workload@sha256:bd73948b02ff44224f60b9deb60118815b00e34ef054ecc0cfb0aa3c9f1ed44a"}
```

Test Container Image

```
docker pull $CONTAINERIMAGE
```

```
docker run -it -p 3001:3001 $CONTAINERIMAGE
```

```
curl localhost:3001
Hello from Node.js Starter Application!%
```

Feed into ec CLI

```
ec validate image --image $CONTAINERIMAGE --policy $ECPOLICY --output yaml
```
