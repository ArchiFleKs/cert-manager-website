---
title: Certificate resource
description: 'cert-manager usage: Certificates'
---

> **apiVersion:** cert-manager.io/v1<br/>
> **kind:** Certificate

<div style={{textAlign: "center"}}>
<object data="/images/request-certificate-overview/request-certificate-cert.svg"></object>
</div>

In cert-manager, the `Certificate` resource represents a human readable definition
of a certificate request. cert-manager uses this input to generate a private key
and [`CertificateRequest`](./certificaterequest.md) resource in order to obtain
a signed certificate from an [`Issuer`](../configuration/README.md) or
[`ClusterIssuer`](../configuration/README.md). The signed certificate and private
key are then stored in the specified `Secret` resource. cert-manager will ensure
that the certificate is [auto-renewed before it expires](#renewal-reissuance) and
[re-issued if requested](#non-renewal-reissuance).

In order to issue any certificates, you'll need to configure an
[`Issuer`](../configuration/README.md) or [`ClusterIssuer`](../configuration/README.md)
resource first.

## Creating Certificate Resources

A `Certificate` resource specifies fields that are used to generate certificate
signing requests which are then fulfilled by the issuer type you have
referenced. `Certificates` specify which issuer they want to obtain the
certificate from by specifying the `certificate.spec.issuerRef` field.

A `Certificate` resource, for the `example.com` and `www.example.com` DNS names,
`spiffe://cluster.local/ns/sandbox/sa/example` URI Subject Alternative Name,
that is valid for 90 days and renews 15 days before expiry is below. It contains
an exhaustive list of all options a `Certificate` resource may have however only
a subset of fields are required as labelled.

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: example-com
  namespace: sandbox
spec:
  # Secret names are always required.
  secretName: example-com-tls

  # secretTemplate is optional. If set, these annotations and labels will be
  # copied to the Secret named example-com-tls. These labels and annotations will
  # be re-reconciled if the Certificate's secretTemplate changes. secretTemplate
  # is also enforced, so relevant label and annotation changes on the Secret by a
  # third party will be overwriten by cert-manager to match the secretTemplate.
  secretTemplate:
    annotations:
      my-secret-annotation-1: "foo"
      my-secret-annotation-2: "bar"
    labels:
      my-secret-label: foo

  privateKey:
    algorithm: RSA
    encoding: PKCS1
    size: 2048

  # keystores allows adding additional output formats. This is an example for reference only.
  keystores:
    pkcs12:
      create: true
      passwordSecretRef:
        name: example-com-tls-keystore
        key: password
      profile: Modern2023

  duration: 2160h # 90d
  renewBefore: 360h # 15d

  isCA: false
  usages:
    - server auth
    - client auth

  subject:
    organizations:
      - cert-manager

  # Avoid using commonName for DNS names in end-entity (leaf) certificates. Unless you have a specific
  # need for it in your environment, use dnsNames exclusively to avoid issues with commonName.
  # Usually, commonName is used to give human-readable names to CA certificates and can be avoided for
  # other certificates.
  commonName: example.com

  # The literalSubject field is exclusive with subject and commonName. It allows
  # specifying the subject directly as a string. This is useful for when the order
  # of the subject fields is important or when the subject contains special types
  # which can be specified by their OID.
  #
  # literalSubject: "O=jetstack, CN=example.com, 2.5.4.42=John, 2.5.4.4=Doe"

  # At least one of commonName (possibly through literalSubject), dnsNames, uris, emailAddresses, ipAddresses or otherNames is required.
  dnsNames:
    - example.com
    - www.example.com
  uris:
    - spiffe://cluster.local/ns/sandbox/sa/example
  emailAddresses:
    - john.doe@cert-manager.io
  ipAddresses:
    - 192.168.0.5
  # Needs cert-manager 1.14+ and "OtherNames" feature flag
  otherNames:
    # Should only supply oid of ut8 valued types
    - oid: 1.3.6.1.4.1.311.20.2.3 # User Principal Name "OID"
      utf8Value: upn@example.local

  # Issuer references are always required.
  issuerRef:
    name: ca-issuer
    # We can reference ClusterIssuers by changing the kind here.
    # The default value is Issuer (i.e. a locally namespaced Issuer)
    kind: Issuer
    # This is optional since cert-manager will default to this value however
    # if you are using an external issuer, change this to that issuer group.
    group: cert-manager.io
```

The signed certificate will be stored in a `Secret` resource named
`example-com-tls` in the same namespace as the `Certificate` once the issuer has
successfully issued the requested certificate.

If `secretTemplate` is present, annotations and labels set in this property
will be copied over to `example-com-tls` secret. Both properties are optional.

The `Certificate` will be issued using the issuer named `ca-issuer` in the
`sandbox` namespace (the same namespace as the `Certificate` resource).

> Note: If you want to create an `Issuer` that can be referenced by
> `Certificate` resources in _all_ namespaces, you should create a
> [`ClusterIssuer`](../concepts/issuer.md#namespaces) resource and set the
> `certificate.spec.issuerRef.kind` field to `ClusterIssuer`.

> Note: The `renewBefore` and `duration` fields must be specified using a [Go
> `time.Duration`](https://golang.org/pkg/time/#ParseDuration) string format,
> which does not allow the `d` (days) suffix. You must specify these values
> using `s`, `m`, and `h` suffixes instead. Failing to do so without installing
> the [`webhook component`](../concepts/webhook.md) can prevent cert-manager
> from functioning correctly
> [`#1269`](https://github.com/cert-manager/cert-manager/issues/1269).

> Note: Take care when setting the `renewBefore` field to be very close to the
> `duration` as this can lead to a renewal loop, where the `Certificate` is always
> in the renewal period. Some `Issuers` set the `notBefore` field on their
> issued X.509 certificates before the issue time to fix clock-skew issues,
> leading to the working duration of a certificate to be less than the full
> duration of the certificate. For example, Let's Encrypt sets it to be one hour
> before issue time, so the actual _working duration_ of the certificate is 89
> days, 23 hours (the _full duration_ remains 90 days).

A full list of the fields supported on the Certificate resource can be found in
the [API reference documentation](../reference/api-docs.md#cert-manager.io/v1.CertificateSpec).

### Target Secret

When a certificate is issued by an intermediate CA and the `Issuer` can provide
the issued certificate's chain, the contents of `tls.crt` will be the requested
certificate followed by the certificate chain.

Additionally, if the Certificate Authority is known, the corresponding CA
certificate will be stored in the secret with key `ca.crt`. For example, with
the ACME issuer, the CA is not known and `ca.crt` will not exist in the Secret.
The `ca.crt` value at the time of issuance can be copied to the trust store of
the application that is using the certificate. However, DO NOT directly mount
the `ca.crt` value into the application's trust store, as it will be updated
when the certificate is renewed (see [Trusting certificates](../trust/README.md) for more details).

cert-manager intentionally avoids adding root certificates to `tls.crt`, because they
are useless in a situation where TLS is being done securely. For more information,
see [RFC 5246 section 7.4.2](https://datatracker.ietf.org/doc/html/rfc5246#section-7.4.2)
which contains the following explanation:

> Because certificate validation requires that root keys be distributed
> independently, the self-signed certificate that specifies the root
> certificate authority MAY be omitted from the chain, under the
> assumption that the remote end must already possess it in order to
> validate it in any case.

<a id="key-usages"></a>
### X.509 key usages and extended key usages

cert-manager supports requesting certificates that have a number of [custom key
usages](https://tools.ietf.org/html/rfc5280#section-4.2.1.3) and [extended key
usages](https://tools.ietf.org/html/rfc5280#section-4.2.1.12). Although
cert-manager will attempt to honor this request, some issuers will remove, add
defaults, or otherwise completely ignore the request.
The `CA` and `SelfSigned` `Issuer` will always return certificates matching the usages you have requested.

Unless any number of usages has been set, cert-manager will set the default
requested usages of `digital signature`, `key encipherment`, and `server auth`.
cert-manager will not attempt to request a new certificate if the current
certificate does not match the current key usage set.

An exhaustive list of supported key usages can be found in the [API reference
documentation](../reference/api-docs.md#cert-manager.io/v1.KeyUsage).


### Additional Certificate Output Formats

`additionalOutputFormats` is a field on the Certificate `spec` that allows
specifying additional supplementary formats of issued certificates and their
private key. There are currently two supported additional output formats:
`CombinedPEM` and `DER`. Both output formats can be specified on the same
Certificate.

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
spec:
  ...
  secretName: my-cert-tls
  additionalOutputFormats:
  - type: CombinedPEM
  - type: DER

# Results in:

apiVersion: v1
kind: Secret
metadata:
  name: my-cert-tls
type: kubernetes.io/tls
data:
  ca.crt: <PEM CA certificate>
  tls.key: <PEM private key>
  tls.crt: <PEM signed certificate chain>
  tls-combined.pem: <PEM private key + "\n" + PEM signed certificate chain>
  key.der: <DER binary format of private key>
```

#### `CombinedPEM`

The `CombinedPEM` type will create a new key entry in the resulting
Certificate's Secret `tls-combined.pem`. This entry will contain the PEM encoded
private key, followed by at least one new line character, followed by the PEM
encoded signed certificate chain-

```text
<private key> + "\n" + <signed certificate chain>
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-cert-tls
type: kubernetes.io/tls
data:
  tls-combined.pem: <PEM private key + "\n" + PEM signed certificate chain>
  ...
```

#### `DER`

The `DER` type will create a new key entry in the resulting Certificate's Secret
`key.der`. This entry will contain the DER binary format of the private key.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-cert-tls
type: kubernetes.io/tls
data:
  key.der: <DER binary format of private key>
  ...
```

### Creating Certificate With Name Constraints

Root or Intermediate CA certificates can have name constraints. Name constraints indicates a name space within which all subject names in subsequent certificates in a certification path MUST be located.
Checkout https://datatracker.ietf.org/doc/html/rfc5280#section-4.2.1.10 for more details on this.

To create a CA Certificate with name constraints use the following configuration:

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: ca-cert-example
spec:
  secretName: example-ca-key-pair
  isCA: true
  issuerRef:
    name: selfsigned
    kind: ClusterIssuer
  commonName: "example1.com"
  dnsNames:
  - example1.com
  nameConstraints:
    critical: true
    permitted:
      dnsDomains: ["example1.com", "example2.com"]
      ipRanges: ["10.10.0.0/16"]
      emailAddress: ["example@example.org"]
    excluded:
      ipRanges: ["10.10.0.0/24"]
```

Note that when used with cert-manager's built-in CA and SelfSigned Issuer, the SANs (DNS name, IP address, URI, and email address) are not checked with the certificate's own name constraints, and are not checked with any of name constraints contained in the chain of certificates the certificate belongs to.

The certificate may get issued successfully, but be rejected by clients during TLS handshakes.

## Issuance triggers

<a id="renewal-reissuance"></a>
### Reissuance triggered by expiry (renewal)

cert-manager will automatically renew `Certificate`s. It will calculate _when_ to renew a `Certificate` based on the issued X.509 certificate's duration and a 'renewBefore' value which specifies _how long_ before expiry a certificate should be renewed.

`spec.duration` and `spec.renewBefore`/`spec.renewBeforePercentage` fields on a `Certificate` can be used to specify an X.509 certificate's duration and a 'renewBefore' value. Default value for `spec.duration` is 90 days. Some issuers might be configured to only issue certificates with a set duration, so the actual duration may be different. `spec.renewBefore` specifies an absolute duration, while `spec.renewBeforePercentage` computes the effective 'renewBefore' using the actual duration of the issued certificate. Using `spec.renewBeforePercentage` is recommended to prevent renewal loops in case the actual duration is less than expected.
Minimum value for `spec.duration` is 1 hour and minimum value for effective `spec.renewBefore` is 5 minutes.
It is also required that `spec.duration` > `spec.renewBefore`.

Once an X.509 certificate has been issued, cert-manager will calculate the renewal time for the `Certificate`. By default this will be 2/3 through the X.509 certificate's duration. If `spec.renewBefore` or `spec.renewBeforePercentage` has been set, it will be the effective `spec.renewBefore` amount of time before expiry. cert-manager will set `Certificate`'s `status.RenewalTime` to the time when the renewal will be attempted.

<a id="non-renewal-reissuance"></a>
<a id="actions-triggering-private-key-rotation"></a>
### Reissuance triggered by user actions

A certificate object is reissued under the following circumstances:

- when a change is made to one of the following fields on the Certificate's
  spec: `commonName`, `dnsNames`, `ipAddresses`, `uris`, `emailAddresses`,
  `subject`, `isCA`, `usages`, `duration` or `issuerRef`;
  A more detailed explanation can be found on the [FAQ page](../faq/README.md#when-do-certs-get-re-issued).
- when a reissuance is manually triggered with the following:
  ```sh
  cmctl renew cert-1
  ```
  Note that the above command requires [cmctl](../reference/cmctl.md#renew).

<div className="warning">

**❌** Deleting the Secret resource associated with a Certificate resource is
**not a recommended solution** for manually rotating the private key. The
recommended way to manually rotate the private key is to trigger the reissuance
of the Certificate resource with the following command (requires
[`cmctl`](../reference/cmctl.md#renew)):

```sh
cmctl renew cert-1
```

</div>

<a id="temporary-certificates-whilst-issuing"></a>
## Issuance behavior: Temporary Certificates while Issuing

When requesting certificates [using the ingress-shim](./ingress.md), the
component `ingress-gce`, if used, requires that a temporary certificate is
present while waiting for the issuance of a signed certificate when serving. To
facilitate this, if the following annotation:

 ```yaml
 cert-manager.io/issue-temporary-certificate: "true"
 ```

is present on the certificate, a self-signed temporary certificate will be
present on the `Secret` until it is overwritten once the signed certificate has
been issued.

Adding the following annotation on an ingress will automatically set "issue-temporary-certificate" on the certificate:

 ```yaml
 acme.cert-manager.io/http01-edit-in-place: "true"
 ```

<a id="rotation-private-key"></a>
## Issuance behavior: Rotation of the private key

> ⚠️ In cert-manager v1.18.0, the default `rotationPolicy` was changed.
>
> In cert-manager `>= v1.18.0` the default is `rotationPolicy: Always`;
> the private key **is** rotated automatically.
>
> In cert-manager `< v1.18.0` the default is `rotationPolicy: Never`;
> the private key **is not** rotated automatically.

With the setting `rotationPolicy: Always`, the private key Secret associated with a Certificate
object can be configured to be rotated as soon as an the Certificate is reissued (see
[Issuance triggers](#issuance-triggers)).

With `rotationPolicy: Always`, cert-manager waits until the Certificate
object is correctly signed before overwriting the `tls.key` file in the
Secret.

With this setting, you can expect **no downtime** if your application can detect
changes to the mounted `tls.crt` and `tls.key` and reload them gracefully or
automatically restart.

If your application only loads the private key and signed certificate once
at start up, the new certificate won't immediately be served by your
application, and you will want to either manually restart your pod with
`kubectl rollout restart`, or automate the action by running
[wave](https://github.com/wave-k8s/wave). Wave is a Secret controller that
makes sure deployments get restarted whenever a mounted Secret changes.

<div className="alert">

Re-use of private keys

Some issuers, like the built-in [Venafi
issuer](../configuration/venafi.md), may disallow re-using private keys.
If this is the case, you must explicitly configure the `rotationPolicy:
Always` setting for each of your Certificate objects accordingly.

</div>

In the following example, the certificate has been set with
`rotationPolicy: Always`:

```yaml
apiVersion: cert-manager.io/v1
kind: Certificate
spec:
  secretName: my-cert-tls
  privateKey:
    rotationPolicy: Always # 🔰 Here.
```

#### The `rotationPolicy` setting

The possible values for `rotationPolicy` are:

| Value                  | Description                                                   |
| ---------------------- | ------------------------------------------------------------- |
| `Never` (default)      | cert-manager reuses the existing private key on each issuance |
| `Always` (recommended) | cert-manager regenerates a new private key on each issuance   |

With `rotationPolicy: Never`, a private key is only generated if one does not
already exist in the target Secret resource (using the `tls.key` key). All
further issuances will re-use this private key. This is the default in order to
maintain compatibility with previous releases.

With `rotationPolicy: Always`, a new private key will be generated each time an
action triggers the reissuance of the certificate object (see [Actions that will
trigger a rotation of the private key](#actions-triggering-private-key-rotation)
above). Note that if the private key secret already exists when creating the
certificate object, the existing private key will not be used, since the
rotation mechanism also includes the initial issuance.

<div className="info">

👉 We recommend that you configure `rotationPolicy: Always` on your Certificate
resources. Rotating both the certificate and the private key simultaneously
prevents the risk of issuing a certificate with an exposed private key. Another
benefit to renewing the private key regularly is to let you be confident that
the private key rotation can be done in case of emergency. More generally, it is
a good practice to be rotating the keys as often as possible, reducing the risk
associated with compromised keys.

</div>

## Cleaning up Secrets when Certificates are deleted

By default, cert-manager does not delete the `Secret` resource containing the signed certificate when the corresponding `Certificate` resource is deleted.
This means that deleting a `Certificate` won't take down any services that are currently relying on that certificate, but the certificate will no longer be renewed.
The `Secret` needs to be manually deleted if it is no longer needed.

If you would prefer the `Secret` to be deleted automatically when the `Certificate` is deleted, you need to configure your installation to pass the `--enable-certificate-owner-ref` flag to the controller.

## Inner workings diagram for developers

<object data="/images/request-certificate-debug/certificate-flow.svg"></object>

[1] https://cert-manager.io/docs/usage/certificaterequest
