```
echo "-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEpXcIGCQmaP7qhEq/xfXT49BNBmTE
AWJvteQ7WiOp1VovrkOlqW64afWtf3qPz70ETXUhZ42lHvg1aKu24vKK/w==
-----END PUBLIC KEY-----" > key.pub

```

```
PUBLIC_KEY=key.pub IMAGE=quay.io/cuipinghuo/hermetic_build:0.3 hack/simple-demo.sh

```