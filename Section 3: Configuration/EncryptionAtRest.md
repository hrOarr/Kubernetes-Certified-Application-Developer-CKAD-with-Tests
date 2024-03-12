**To secure sensitive data stored in Kubernetes resources (e.g. Secrets), that data can be encrypted at rest. In Kubernetes this means that data is encrypted while stored in etcd and is only decrypted when the resource is requested via a Kubernetes API request.**

*This feature is in an early stage and considered a preview feature. It is **not recommended** to enable this for production environments due to potential data loss.*


## Available Encryption Providers
 - Secretbox

## Declarative approach
```
# snippet for directly passing a key
spec:
  encryptionConfiguration:
    enabled: true
    resources:
      - secrets
    secretbox:
      keys:
        - name: encryption-key-2022-01
          value: ynCl8otobs5NuHu$3TLghqwFXVpv6N//SE6ZVTimYok=

# snippet for referencing a secret
spec:
  encryptionConfiguration:
    enabled: true
    resources:
      - secrets
    secretbox:
      keys:
        - name: encryption-key-2022-01
          secretRef:
            name: encryption-key-2022-01
            key: key
```
