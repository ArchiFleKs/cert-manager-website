---
title: API Reference
description: >-
  cert-manager API documentation, including Custom Resources such as
  Certificate, CertificateRequest, Issuer and ClusterIssuer
---
<p>cert-manager API documentation, including various Custom Resource Definitions</p>
<p>Packages:</p>
<ul>
  <li>
    <a href="#acme.cert-manager.io%2fv1">acme.cert-manager.io/v1</a>
  </li>
  <li>
    <a href="#cainjector.config.cert-manager.io%2fv1alpha1">cainjector.config.cert-manager.io/v1alpha1</a>
  </li>
  <li>
    <a href="#cert-manager.io%2fv1">cert-manager.io/v1</a>
  </li>
  <li>
    <a href="#controller.config.cert-manager.io%2fv1alpha1">controller.config.cert-manager.io/v1alpha1</a>
  </li>
  <li>
    <a href="#meta.cert-manager.io%2fv1">meta.cert-manager.io/v1</a>
  </li>
  <li>
    <a href="#webhook.config.cert-manager.io%2fv1alpha1">webhook.config.cert-manager.io/v1alpha1</a>
  </li>
</ul>
<h2 id="acme.cert-manager.io/v1">acme.cert-manager.io/v1</h2>
<div>
  <p>Package v1 is the v1 version of the API.</p>
</div>
<p>Resource Types:</p>
<ul>
  <li>
    <a href="#acme.cert-manager.io/v1.Challenge">Challenge</a>
  </li>
  <li>
    <a href="#acme.cert-manager.io/v1.Order">Order</a>
  </li>
</ul>
<h3 id="acme.cert-manager.io/v1.Challenge">Challenge</h3>
<div>
  <p>Challenge is a type to represent a Challenge request with an ACME server</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>acme.cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>Challenge</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ChallengeSpec">ChallengeSpec</a>
        </em>
      </td>
      <td>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>url</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p>The URL of the ACME Challenge resource for this challenge. This can be used to lookup details about the status of this challenge.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>authorizationURL</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p>The URL to the ACME Authorization resource that this challenge is a part of.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>dnsName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p> dnsName is the identifier that this challenge is for, e.g., example.com. If the requested DNSName is a &lsquo;wildcard&rsquo;, this field MUST be set to the non-wildcard domain, e.g., for <code>*.example.com</code>, it must be <code>example.com</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>wildcard</code>
              <br />
              <em>bool</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>wildcard will be true if this challenge is for a wildcard identifier, for example &lsquo;*.example.com&rsquo;.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>type</code>
              <br />
              <em>
                <a href="#acme.cert-manager.io/v1.ACMEChallengeType">ACMEChallengeType</a>
              </em>
            </td>
            <td>
              <p>The type of ACME challenge this resource represents. One of &ldquo;HTTP-01&rdquo; or &ldquo;DNS-01&rdquo;.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>token</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p>The ACME challenge token for this challenge. This is the raw value returned from the ACME server.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>key</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p>
                The ACME challenge key for this challenge For HTTP01 challenges, this is the value that must be responded with to complete the HTTP01 challenge in the format:
                <code>&lt;private key JWK thumbprint&gt;.&lt;key from acme server for challenge&gt;</code>. For DNS01 challenges, this is the base64 encoded SHA256 sum of the
                <code>&lt;private key JWK thumbprint&gt;.&lt;key from acme server for challenge&gt;</code>
                text that must be set as the TXT record content.
              </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>solver</code>
              <br />
              <em>
                <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</a>
              </em>
            </td>
            <td>
              <p>Contains the domain solving configuration that should be used to solve this challenge resource.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>issuerRef</code>
              <br />
              <em>
                <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
              </em>
            </td>
            <td>
              <p>References a properly configured ACME-type Issuer which should be used to create this Challenge. If the Issuer does not exist, processing will be retried. If the Issuer is not an &lsquo;ACME&rsquo; Issuer, an error will be returned and the Challenge will be marked as failed.</p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ChallengeStatus">ChallengeStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.Order">Order</h3>
<div>
  <p>Order is a type to represent an Order with an ACME server</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>acme.cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>Order</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.OrderSpec">OrderSpec</a>
        </em>
      </td>
      <td>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>request</code>
              <br />
              <em>[]byte</em>
            </td>
            <td>
              <p>Certificate signing request bytes in DER encoding. This will be used when finalizing the order. This field must be set on the order.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>issuerRef</code>
              <br />
              <em>
                <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
              </em>
            </td>
            <td>
              <p>IssuerRef references a properly configured ACME-type Issuer which should be used to create this Order. If the Issuer does not exist, processing will be retried. If the Issuer is not an &lsquo;ACME&rsquo; Issuer, an error will be returned and the Order will be marked as failed.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>commonName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> CommonName is the common name as specified on the DER encoded CSR. If specified, this value must also be present in <code>dnsNames</code> or <code>ipAddresses</code>. This field must match the corresponding field on the DER encoded CSR. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>dnsNames</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>DNSNames is a list of DNS names that should be included as part of the Order validation process. This field must match the corresponding field on the DER encoded CSR.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>ipAddresses</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>IPAddresses is a list of IP addresses that should be included as part of the Order validation process. This field must match the corresponding field on the DER encoded CSR.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>duration</code>
              <br />
              <em>
                <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Duration is the duration for the not after date for the requested certificate. this is set on order creation as pe the ACME spec.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>profile</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Profile allows requesting a certificate profile from the ACME server. Supported profiles are listed by the server&rsquo;s ACME directory URL.</p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.OrderStatus">OrderStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEAuthorization">ACMEAuthorization</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.OrderStatus">OrderStatus</a>) </p>
<div>
  <p>ACMEAuthorization contains data returned from the ACME server on an authorization that must be completed in order validate a DNS name on an ACME Order resource.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>URL is the URL of the Authorization that must be completed</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>identifier</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Identifier is the DNS name to be validated as part of this authorization</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>wildcard</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Wildcard will be true if this authorization is for a wildcard DNS name. If this is true, the identifier will be the <em>non-wildcard</em> version of the DNS name. For example, if &lsquo;*.example.com&rsquo; is the DNS name being validated, this field will be &lsquo;true&rsquo; and the &lsquo;identifier&rsquo; field will be &lsquo;example.com&rsquo;. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>initialState</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.State">State</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>InitialState is the initial state of the ACME authorization when first fetched from the ACME server. If an Authorization is already &lsquo;valid&rsquo;, the Order controller will not create a Challenge resource for the authorization. This will occur when working with an ACME server that enables &lsquo;authz reuse&rsquo; (such as Let&rsquo;s Encrypt&rsquo;s production endpoint). If not set and &lsquo;identifier&rsquo; is set, the state is assumed to be pending and a Challenge will be created.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>challenges</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallenge">[]ACMEChallenge</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Challenges specifies the challenge types offered by the ACME server. One of these challenge types will be selected when validating the DNS name and an appropriate Challenge resource will be created to perform the ACME challenge process.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallenge">ACMEChallenge</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEAuthorization">ACMEAuthorization</a>) </p>
<div>
  <p>Challenge specifies a challenge offered by the ACME server for an Order. An appropriate Challenge resource can be created to perform the ACME challenge process.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>URL is the URL of this challenge. It can be used to retrieve additional metadata about the Challenge from the ACME server.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>token</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Token is the token that must be presented for this challenge. This is used to compute the &lsquo;key&rsquo; that must also be presented.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Type is the type of challenge being offered, e.g., &lsquo;http-01&rsquo;, &lsquo;dns-01&rsquo;, &lsquo;tls-sni-01&rsquo;, etc. This is the raw value retrieved from the ACME server. Only &lsquo;http-01&rsquo; and &lsquo;dns-01&rsquo; are supported by cert-manager, other values will be ignored.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEIssuer">ACMEIssuer</a>, <a href="#acme.cert-manager.io/v1.ChallengeSpec">ChallengeSpec</a>) </p>
<div>
  <p>An ACMEChallengeSolver describes how to solve ACME challenges for the issuer it is part of. A selector may be provided to use different solving strategies for different DNS names. Only one of HTTP01 or DNS01 must be provided.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>selector</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.CertificateDNSNameSelector">CertificateDNSNameSelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Selector selects a set of DNSNames on the Certificate resource that should be solved using this challenge solver. If not specified, the solver will be treated as the &lsquo;default&rsquo; solver with the lowest priority, i.e. if any other solver has a more specific match, it will be used instead.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>http01</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01">ACMEChallengeSolverHTTP01</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Configures cert-manager to attempt to complete authorizations by performing the HTTP01 challenge flow. It is not possible to obtain certificates for wildcard domain names (e.g., <code>*.example.com</code>) using the HTTP01 challenge mechanism. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dns01</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Configures cert-manager to attempt to complete authorizations by performing the DNS01 challenge flow.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</a>) </p>
<div>
  <p>Used to configure a DNS01 challenge provider to be used when solving DNS01 challenges. Only one DNS provider may be configured per solver.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>cnameStrategy</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.CNAMEStrategy">CNAMEStrategy</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>CNAMEStrategy configures how the DNS01 provider should handle CNAME records when found in DNS zones.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>akamai</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAkamai">ACMEIssuerDNS01ProviderAkamai</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the Akamai DNS zone management API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>cloudDNS</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudDNS">ACMEIssuerDNS01ProviderCloudDNS</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the Google Cloud DNS API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>cloudflare</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudflare">ACMEIssuerDNS01ProviderCloudflare</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the Cloudflare API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>route53</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRoute53">ACMEIssuerDNS01ProviderRoute53</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the AWS Route53 API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>azureDNS</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAzureDNS">ACMEIssuerDNS01ProviderAzureDNS</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the Microsoft Azure DNS API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>digitalocean</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderDigitalOcean">ACMEIssuerDNS01ProviderDigitalOcean</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Use the DigitalOcean DNS API to manage DNS01 challenge records.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>acmeDNS</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAcmeDNS">ACMEIssuerDNS01ProviderAcmeDNS</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Use the &lsquo;ACME DNS&rsquo; (<a href="https://github.com/joohoi/acme-dns">https://github.com/joohoi/acme-dns</a>) API to manage DNS01 challenge records. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>rfc2136</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRFC2136">ACMEIssuerDNS01ProviderRFC2136</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Use RFC2136 (&ldquo;Dynamic Updates in the Domain Name System&rdquo;) (<a href="https://datatracker.ietf.org/doc/rfc2136/">https://datatracker.ietf.org/doc/rfc2136/</a>) to manage DNS01 challenge records. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>webhook</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderWebhook">ACMEIssuerDNS01ProviderWebhook</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Configure an external webhook based DNS01 challenge solver to manage DNS01 challenge records.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01">ACMEChallengeSolverHTTP01</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</a>) </p>
<div>
  <p>ACMEChallengeSolverHTTP01 contains configuration detailing how to solve HTTP01 challenges within a Kubernetes cluster. Typically this is accomplished through creating &lsquo;routes&rsquo; of some description that configure ingress controllers to direct traffic to &lsquo;solver pods&rsquo;, which are responsible for responding to the ACME server&rsquo;s HTTP requests. Only one of Ingress / Gateway can be specified.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>ingress</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01Ingress">ACMEChallengeSolverHTTP01Ingress</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The ingress based HTTP01 challenge solver will solve challenges by creating or modifying Ingress resources in order to route requests for &lsquo;/.well-known/acme-challenge/XYZ&rsquo; to &lsquo;challenge solver&rsquo; pods that are provisioned by cert-manager for each Challenge to be completed.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>gatewayHTTPRoute</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01GatewayHTTPRoute">ACMEChallengeSolverHTTP01GatewayHTTPRoute</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The Gateway API is a sig-network community API that models service networking in Kubernetes (<a href="https://gateway-api.sigs.k8s.io/">https://gateway-api.sigs.k8s.io/</a>). The Gateway solver will create HTTPRoutes with the specified labels in the same namespace as the challenge. This solver is experimental, and fields / behaviour may change in the future. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01GatewayHTTPRoute">ACMEChallengeSolverHTTP01GatewayHTTPRoute</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01">ACMEChallengeSolverHTTP01</a>) </p>
<div>
  <p>The ACMEChallengeSolverHTTP01GatewayHTTPRoute solver will create HTTPRoute objects for a Gateway class routing to an ACME challenge solver pod.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>serviceType</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#servicetype-v1-core">Kubernetes core/v1.ServiceType</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Optional service type for Kubernetes solver service. Supported values are NodePort or ClusterIP. If unset, defaults to NodePort.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>labels</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Custom labels that will be applied to HTTPRoutes created by cert-manager while solving HTTP-01 challenges.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>parentRefs</code>
        <br />
        <em>[]sigs.k8s.io/gateway-api/apis/v1.ParentReference</em>
      </td>
      <td>
        <p>
          When solving an HTTP-01 challenge, cert-manager creates an HTTPRoute. cert-manager needs to know which parentRefs should be used when creating the HTTPRoute. Usually, the parentRef references a Gateway. See:
          <a href="https://gateway-api.sigs.k8s.io/api-types/httproute/#attaching-to-gateways">https://gateway-api.sigs.k8s.io/api-types/httproute/#attaching-to-gateways</a>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>podTemplate</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodTemplate">ACMEChallengeSolverHTTP01IngressPodTemplate</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Optional pod template used to configure the ACME challenge solver pods used for HTTP01 challenges.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01Ingress">ACMEChallengeSolverHTTP01Ingress</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01">ACMEChallengeSolverHTTP01</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>serviceType</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#servicetype-v1-core">Kubernetes core/v1.ServiceType</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Optional service type for Kubernetes solver service. Supported values are NodePort or ClusterIP. If unset, defaults to NodePort.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ingressClassName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> This field configures the field <code>ingressClassName</code> on the created Ingress resources used to solve ACME challenges that use this challenge solver. This is the recommended way of configuring the ingress class. Only one of <code>class</code>, <code>name</code> or <code>ingressClassName</code> may be specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>class</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> This field configures the annotation <code>kubernetes.io/ingress.class</code> when creating Ingress resources to solve ACME challenges that use this challenge solver. Only one of <code>class</code>, <code>name</code> or <code>ingressClassName</code> may be specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The name of the ingress resource that should have ACME challenge solving routes inserted into it in order to solve HTTP01 challenges. This is typically used in conjunction with ingress controllers like ingress-gce, which maintains a 1:1 mapping between external IPs and ingress resources. Only one of <code>class</code>, <code>name</code> or <code>ingressClassName</code> may be specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>podTemplate</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodTemplate">ACMEChallengeSolverHTTP01IngressPodTemplate</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Optional pod template used to configure the ACME challenge solver pods used for HTTP01 challenges.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ingressTemplate</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressTemplate">ACMEChallengeSolverHTTP01IngressTemplate</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Optional ingress template used to configure the ACME challenge solver ingress used for HTTP01 challenges.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressObjectMeta">ACMEChallengeSolverHTTP01IngressObjectMeta</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressTemplate">ACMEChallengeSolverHTTP01IngressTemplate</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>annotations</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Annotations that should be added to the created ACME HTTP01 solver ingress.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>labels</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Labels that should be added to the created ACME HTTP01 solver ingress.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodObjectMeta">ACMEChallengeSolverHTTP01IngressPodObjectMeta</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodTemplate">ACMEChallengeSolverHTTP01IngressPodTemplate</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>annotations</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Annotations that should be added to the created ACME HTTP01 solver pods.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>labels</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Labels that should be added to the created ACME HTTP01 solver pods.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSecurityContext">ACMEChallengeSolverHTTP01IngressPodSecurityContext</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSpec">ACMEChallengeSolverHTTP01IngressPodSpec</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>seLinuxOptions</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#selinuxoptions-v1-core">Kubernetes core/v1.SELinuxOptions</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The SELinux context to be applied to all containers. If unspecified, the container runtime will allocate a random SELinux context for each container. May also be set in SecurityContext. If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence for that container. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>runAsUser</code>
        <br />
        <em>int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The UID to run the entrypoint of the container process. Defaults to user specified in image metadata if unspecified. May also be set in SecurityContext. If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence for that container. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>runAsGroup</code>
        <br />
        <em>int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The GID to run the entrypoint of the container process. Uses runtime default if unset. May also be set in SecurityContext. If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence for that container. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>runAsNonRoot</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Indicates that the container must run as a non-root user. If true, the Kubelet will validate the image at runtime to ensure that it does not run as UID 0 (root) and fail to start the container if it does. If unset or false, no such validation will be performed. May also be set in SecurityContext. If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>supplementalGroups</code>
        <br />
        <em>[]int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>A list of groups applied to the first process run in each container, in addition to the container&rsquo;s primary GID, the fsGroup (if specified), and group memberships defined in the container image for the uid of the container process. If unspecified, no additional groups are added to any container. Note that group memberships defined in the container image for the uid of the container process are still effective, even if they are not included in this list. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>fsGroup</code>
        <br />
        <em>int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>A special supplemental group that applies to all containers in a pod. Some volume types allow the Kubelet to change the ownership of that volume to be owned by the pod:</p>
        <ol>
          <li>The owning GID will be the FSGroup</li>
          <li>The setgid bit is set (new files created in the volume will be owned by FSGroup)</li>
          <li>The permission bits are OR&rsquo;d with rw-rw&mdash;-</li>
        </ol>
        <p>If unset, the Kubelet will not modify the ownership and permissions of any volume. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>sysctls</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#sysctl-v1-core">[]Kubernetes core/v1.Sysctl</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Sysctls hold a list of namespaced sysctls used for the pod. Pods with unsupported sysctls (by the container runtime) might fail to launch. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>fsGroupChangePolicy</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#podfsgroupchangepolicy-v1-core">Kubernetes core/v1.PodFSGroupChangePolicy</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>fsGroupChangePolicy defines behavior of changing ownership and permission of the volume before being exposed inside Pod. This field will only apply to volume types which support fsGroup based ownership(and permissions). It will have no effect on ephemeral volume types such as: secret, configmaps and emptydir. Valid values are &ldquo;OnRootMismatch&rdquo; and &ldquo;Always&rdquo;. If not specified, &ldquo;Always&rdquo; is used. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>seccompProfile</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#seccompprofile-v1-core">Kubernetes core/v1.SeccompProfile</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The seccomp options to use by the containers in this pod. Note that this field cannot be set when spec.os.name is windows.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSpec">ACMEChallengeSolverHTTP01IngressPodSpec</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodTemplate">ACMEChallengeSolverHTTP01IngressPodTemplate</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>nodeSelector</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> NodeSelector is a selector which must be true for the pod to fit on a node. Selector which must match a node&rsquo;s labels for the pod to be scheduled on that node. More info: <a href="https://kubernetes.io/docs/concepts/configuration/assign-pod-node/">https://kubernetes.io/docs/concepts/configuration/assign-pod-node/</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>affinity</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#affinity-v1-core">Kubernetes core/v1.Affinity</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s scheduling constraints</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tolerations</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#toleration-v1-core">[]Kubernetes core/v1.Toleration</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s tolerations.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>priorityClassName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s priorityClassName.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>serviceAccountName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s service account</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>imagePullSecrets</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#localobjectreference-v1-core">[]Kubernetes core/v1.LocalObjectReference</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s imagePullSecrets</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>securityContext</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSecurityContext">ACMEChallengeSolverHTTP01IngressPodSecurityContext</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If specified, the pod&rsquo;s security context</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodTemplate">ACMEChallengeSolverHTTP01IngressPodTemplate</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01GatewayHTTPRoute">ACMEChallengeSolverHTTP01GatewayHTTPRoute</a>, <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01Ingress">ACMEChallengeSolverHTTP01Ingress</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodObjectMeta">ACMEChallengeSolverHTTP01IngressPodObjectMeta</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ObjectMeta overrides for the pod used to solve HTTP01 challenges. Only the &lsquo;labels&rsquo; and &lsquo;annotations&rsquo; fields may be set. If labels or annotations overlap with in-built values, the values here will override the in-built values.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSpec">ACMEChallengeSolverHTTP01IngressPodSpec</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>PodSpec defines overrides for the HTTP01 challenge solver pod. Check ACMEChallengeSolverHTTP01IngressPodSpec to find out currently supported fields. All other fields will be ignored.</p>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>nodeSelector</code>
              <br />
              <em>map[string]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> NodeSelector is a selector which must be true for the pod to fit on a node. Selector which must match a node&rsquo;s labels for the pod to be scheduled on that node. More info: <a href="https://kubernetes.io/docs/concepts/configuration/assign-pod-node/">https://kubernetes.io/docs/concepts/configuration/assign-pod-node/</a> </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>affinity</code>
              <br />
              <em>
                <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#affinity-v1-core">Kubernetes core/v1.Affinity</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s scheduling constraints</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>tolerations</code>
              <br />
              <em>
                <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#toleration-v1-core">[]Kubernetes core/v1.Toleration</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s tolerations.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>priorityClassName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s priorityClassName.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>serviceAccountName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s service account</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>imagePullSecrets</code>
              <br />
              <em>
                <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#localobjectreference-v1-core">[]Kubernetes core/v1.LocalObjectReference</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s imagePullSecrets</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>securityContext</code>
              <br />
              <em>
                <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressPodSecurityContext">ACMEChallengeSolverHTTP01IngressPodSecurityContext</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>If specified, the pod&rsquo;s security context</p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressTemplate">ACMEChallengeSolverHTTP01IngressTemplate</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01Ingress">ACMEChallengeSolverHTTP01Ingress</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverHTTP01IngressObjectMeta">ACMEChallengeSolverHTTP01IngressObjectMeta</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ObjectMeta overrides for the ingress used to solve HTTP01 challenges. Only the &lsquo;labels&rsquo; and &lsquo;annotations&rsquo; fields may be set. If labels or annotations overlap with in-built values, the values here will override the in-built values.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEChallengeType"> ACMEChallengeType (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ChallengeSpec">ChallengeSpec</a>) </p>
<div>
  <p>The type of ACME challenge. Only HTTP-01 and DNS-01 are supported.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;DNS-01&#34;</p>
      </td>
      <td>
        <p> ACMEChallengeTypeDNS01 denotes a Challenge is of type dns-01 More info: <a href="https://letsencrypt.org/docs/challenge-types/#dns-01-challenge">https://letsencrypt.org/docs/challenge-types/#dns-01-challenge</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;HTTP-01&#34;</p>
      </td>
      <td>
        <p> ACMEChallengeTypeHTTP01 denotes a Challenge is of type http-01 More info: <a href="https://letsencrypt.org/docs/challenge-types/#http-01-challenge">https://letsencrypt.org/docs/challenge-types/#http-01-challenge</a> </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEExternalAccountBinding">ACMEExternalAccountBinding</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEIssuer">ACMEIssuer</a>) </p>
<div>
  <p>ACMEExternalAccountBinding is a reference to a CA external account of the ACME server.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>keyID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>keyID is the ID of the CA key that the External Account is bound to.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>keySecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <p> keySecretRef is a Secret Key Selector referencing a data item in a Kubernetes Secret which holds the symmetric MAC key of the External Account Binding. The <code>key</code> is the index string that is paired with the key data in the Secret and should not be confused with the key data itself, or indeed with the External Account Binding keyID above. The secret key stored in the Secret <strong>must</strong> be un-padded, base64 URL encoded data. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>keyAlgorithm</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.HMACKeyAlgorithm">HMACKeyAlgorithm</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Deprecated: keyAlgorithm field exists for historical compatibility reasons and should not be used. The algorithm is now hardcoded to HS256 in golang/x/crypto/acme.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuer">ACMEIssuer</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>) </p>
<div>
  <p>ACMEIssuer contains the specification for an ACME issuer. This uses the RFC8555 specification to obtain certificates by completing &lsquo;challenges&rsquo; to prove ownership of domain identifiers. Earlier draft versions of the ACME specification are not supported.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>email</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Email is the email address to be associated with the ACME account. This field is optional, but it is strongly recommended to be set. It will be used to contact you in case of issues with your account or certificates, including expiry notification emails. This field may be updated after the account is initially registered.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>server</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> Server is the URL used to access the ACME server&rsquo;s &lsquo;directory&rsquo; endpoint. For example, for Let&rsquo;s Encrypt&rsquo;s staging endpoint, you would use: &ldquo;<a href='https://acme-staging-v02.api.letsencrypt.org/directory"'>https://acme-staging-v02.api.letsencrypt.org/directory&rdquo;</a>. Only ACME v2 endpoints (i.e. RFC 8555) are supported. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>preferredChain</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>PreferredChain is the chain to use if the ACME server outputs multiple. PreferredChain is no guarantee that this one gets delivered by the ACME endpoint. For example, for Let&rsquo;s Encrypt&rsquo;s DST cross-sign you would use: &ldquo;DST Root CA X3&rdquo; or &ldquo;ISRG Root X1&rdquo; for the newer Let&rsquo;s Encrypt root CA. This value picks the first certificate bundle in the combined set of ACME default and alternative chains that has a root-most certificate with this value as its issuer&rsquo;s commonname.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>caBundle</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Base64-encoded bundle of PEM CAs which can be used to validate the certificate chain presented by the ACME server. Mutually exclusive with SkipTLSVerify; prefer using CABundle to prevent various kinds of security vulnerabilities. If CABundle and SkipTLSVerify are unset, the system certificate bundle inside the container is used to validate the TLS connection.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>skipTLSVerify</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>INSECURE: Enables or disables validation of the ACME server TLS certificate. If true, requests to the ACME server will not have the TLS certificate chain validated. Mutually exclusive with CABundle; prefer using CABundle to prevent various kinds of security vulnerabilities. Only enable this option in development environments. If CABundle and SkipTLSVerify are unset, the system certificate bundle inside the container is used to validate the TLS connection. Defaults to false.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>externalAccountBinding</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEExternalAccountBinding">ACMEExternalAccountBinding</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ExternalAccountBinding is a reference to a CA external account of the ACME server. If set, upon registration cert-manager will attempt to associate the given external account credentials with the registered ACME account.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>privateKeySecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <p> PrivateKey is the name of a Kubernetes Secret resource that will be used to store the automatically generated ACME account private key. Optionally, a <code>key</code> may be specified to select a specific entry within the named Secret resource. If <code>key</code> is not specified, a default of <code>tls.key</code> will be used. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solvers</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">[]ACMEChallengeSolver</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Solvers is a list of challenge solvers that will be used to solve ACME challenges for the matching domains. Solver configurations must be provided in order to obtain certificates from an ACME server. For more information, see: <a href="https://cert-manager.io/docs/configuration/acme/">https://cert-manager.io/docs/configuration/acme/</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>disableAccountKeyGeneration</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Enables or disables generating a new ACME account key. If true, the Issuer resource will <em>not</em> request a new account but will expect the account key to be supplied via an existing secret. If false, the cert-manager system will generate a new ACME account key for the Issuer. Defaults to false. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enableDurationFeature</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Enables requesting a Not After date on certificates that matches the duration of the certificate. This is not supported by all ACME servers like Let&rsquo;s Encrypt. If set to true when the ACME server does not support it, it will create an error on the Order. Defaults to false.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>profile</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Profile allows requesting a certificate profile from the ACME server. Supported profiles are listed by the server&rsquo;s ACME directory URL.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAcmeDNS">ACMEIssuerDNS01ProviderAcmeDNS</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderAcmeDNS is a structure containing the configuration for ACME-DNS servers</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>host</code>
        <br />
        <em>string</em>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <code>accountSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAkamai">ACMEIssuerDNS01ProviderAkamai</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderAkamai is a structure containing the DNS configuration for Akamai DNS—Zone Record Management API</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>serviceConsumerDomain</code>
        <br />
        <em>string</em>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <code>clientTokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <code>clientSecretSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <code>accessTokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAzureDNS">ACMEIssuerDNS01ProviderAzureDNS</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderAzureDNS is a structure containing the configuration for Azure DNS</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>clientID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Auth: Azure Service Principal: The ClientID of the Azure Service Principal used to authenticate with Azure DNS. If set, ClientSecret and TenantID must also be set.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clientSecretSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Auth: Azure Service Principal: A reference to a Secret containing the password associated with the Service Principal. If set, ClientID and TenantID must also be set.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>subscriptionID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>ID of the Azure subscription</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tenantID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Auth: Azure Service Principal: The TenantID of the Azure Service Principal used to authenticate with Azure DNS. If set, ClientID and ClientSecret must also be set.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>resourceGroupName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>resource group the DNS zone is located in</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>hostedZoneName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>name of the DNS zone that should be used</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>environment</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.AzureDNSEnvironment">AzureDNSEnvironment</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>name of the Azure environment (default AzurePublicCloud)</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>managedIdentity</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.AzureManagedIdentity">AzureManagedIdentity</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Auth: Azure Workload Identity or Azure Managed Service Identity: Settings to enable Azure Workload Identity or Azure Managed Service Identity If set, ClientID, ClientSecret and TenantID must not be set.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudDNS">ACMEIssuerDNS01ProviderCloudDNS</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderCloudDNS is a structure containing the DNS configuration for Google Cloud DNS</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>serviceAccountSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
      </td>
    </tr>
    <tr>
      <td>
        <code>project</code>
        <br />
        <em>string</em>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <code>hostedZoneName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>HostedZoneName is an optional field that tells cert-manager in which Cloud DNS zone the challenge record has to be created. If left empty cert-manager will automatically choose a zone.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudflare">ACMEIssuerDNS01ProviderCloudflare</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p> ACMEIssuerDNS01ProviderCloudflare is a structure containing the DNS configuration for Cloudflare. One of <code>apiKeySecretRef</code> or <code>apiTokenSecretRef</code> must be provided. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>email</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Email of the account, only required when using API key based authentication.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiKeySecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>API key to use to authenticate with Cloudflare. Note: using an API token to authenticate is now the recommended method as it allows greater control of permissions.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiTokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>API token used to authenticate with Cloudflare.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderDigitalOcean">ACMEIssuerDNS01ProviderDigitalOcean</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderDigitalOcean is a structure containing the DNS configuration for DigitalOcean Domains</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>tokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRFC2136">ACMEIssuerDNS01ProviderRFC2136</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderRFC2136 is a structure containing the configuration for RFC2136 DNS</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>nameserver</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The IP address or hostname of an authoritative DNS server supporting RFC2136 in the form host:port. If the host is an IPv6 address it must be enclosed in square brackets (e.g [2001:db8::1]) ; port is optional. This field is required.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tsigSecretSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The name of the secret containing the TSIG value. If <code>tsigKeyName</code> is defined, this field is required. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tsigKeyName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The TSIG Key name configured in the DNS. If <code>tsigSecretSecretRef</code> is defined, this field is required. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tsigAlgorithm</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The TSIG Algorithm configured in the DNS supporting RFC2136. Used only when <code>tsigSecretSecretRef</code> and <code>tsigKeyName</code> are defined. Supported values are (case-insensitive): <code>HMACMD5</code> (default), <code>HMACSHA1</code>, <code>HMACSHA256</code> or <code>HMACSHA512</code>. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRoute53">ACMEIssuerDNS01ProviderRoute53</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderRoute53 is a structure containing the Route 53 configuration for AWS</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>auth</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.Route53Auth">Route53Auth</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Auth configures how cert-manager authenticates.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>accessKeyID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The AccessKeyID is used for authentication. Cannot be set when SecretAccessKeyID is set. If neither the Access Key nor Key ID are set, we fall-back to using env vars, shared credentials file or AWS Instance metadata, see: <a href="https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials">https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>accessKeyIDSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The SecretAccessKey is used for authentication. If set, pull the AWS access key ID from a key within a Kubernetes Secret. Cannot be set when AccessKeyID is set. If neither the Access Key nor Key ID are set, we fall-back to using env vars, shared credentials file or AWS Instance metadata, see: <a href="https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials">https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretAccessKeySecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The SecretAccessKey is used for authentication. If neither the Access Key nor Key ID are set, we fall-back to using env vars, shared credentials file or AWS Instance metadata, see: <a href="https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials">https://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/configuring-sdk.html#specifying-credentials</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>role</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Role is a Role ARN which the Route53 provider will assume using either the explicit credentials AccessKeyID/SecretAccessKey or the inferred credentials from environment variables, shared credentials file or AWS Instance metadata</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>hostedZoneID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If set, the provider will manage only this zone in Route53 and will not do a lookup using the route53:ListHostedZonesByName api call.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>region</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Override the AWS region.</p>
        <p> Route53 is a global service and does not have regional endpoints but the region specified here (or via environment variables) is used as a hint to help compute the correct AWS credential scope and partition when it connects to Route53. See: - <a href="https://docs.aws.amazon.com/general/latest/gr/r53.html">Amazon Route 53 endpoints and quotas</a>- <a href="https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/global-services.html">Global services</a> </p>
        <p>If you omit this region field, cert-manager will use the region from AWS_REGION and AWS_DEFAULT_REGION environment variables, if they are set in the cert-manager controller Pod.</p>
        <p> The <code>region</code> field is not needed if you use <a href="https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html">IAM Roles for Service Accounts (IRSA)</a>. Instead an AWS_REGION environment variable is added to the cert-manager controller Pod by: <a href="https://github.com/aws/amazon-eks-pod-identity-webhook">Amazon EKS Pod Identity Webhook</a>. In this case this <code>region</code> field value is ignored. </p>
        <p> The <code>region</code> field is not needed if you use <a href="https://docs.aws.amazon.com/eks/latest/userguide/pod-identities.html">EKS Pod Identities</a>. Instead an AWS_REGION environment variable is added to the cert-manager controller Pod by: <a href="https://github.com/aws/eks-pod-identity-agent">Amazon EKS Pod Identity Agent</a>, In this case this <code>region</code> field value is ignored. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderWebhook">ACMEIssuerDNS01ProviderWebhook</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>ACMEIssuerDNS01ProviderWebhook specifies configuration for a webhook DNS01 provider, including where to POST ChallengePayload resources.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>groupName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The API group name that should be used when POSTing ChallengePayload resources to the webhook apiserver. This should be the same as the GroupName specified in the webhook provider implementation.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The name of the solver to use, as defined in the webhook provider implementation. This will typically be the name of the provider, e.g., &lsquo;cloudflare&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>config</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#json-v1-apiextensions">Kubernetes apiextensions/v1.JSON</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Additional configuration that should be passed to the webhook apiserver when challenges are processed. This can contain arbitrary JSON data. Secret values should not be specified in this stanza. If secret values are needed (e.g., credentials for a DNS service), you should use a SecretKeySelector to reference a Secret resource. For details on the schema of this field, consult the webhook provider implementation&rsquo;s documentation.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ACMEIssuerStatus">ACMEIssuerStatus</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerStatus">IssuerStatus</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>uri</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>URI is the unique account identifier, which can also be used to retrieve account details from the CA</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastRegisteredEmail</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastRegisteredEmail is the email associated with the latest registered ACME account, in order to track changes made to registered account associated with the Issuer</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastPrivateKeyHash</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastPrivateKeyHash is a hash of the private key associated with the latest registered ACME account, in order to track changes made to registered account associated with the Issuer</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.AzureDNSEnvironment"> AzureDNSEnvironment (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAzureDNS">ACMEIssuerDNS01ProviderAzureDNS</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;AzureChinaCloud&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;AzureGermanCloud&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;AzurePublicCloud&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;AzureUSGovernmentCloud&#34;</p>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.AzureManagedIdentity">AzureManagedIdentity</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAzureDNS">ACMEIssuerDNS01ProviderAzureDNS</a>) </p>
<div>
  <p>AzureManagedIdentity contains the configuration for Azure Workload Identity or Azure Managed Service Identity If the AZURE_FEDERATED_TOKEN_FILE environment variable is set, the Azure Workload Identity will be used. Otherwise, we fall-back to using Azure Managed Service Identity.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>clientID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>client ID of the managed identity, cannot be used at the same time as resourceID</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>resourceID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>resource ID of the managed identity, cannot be used at the same time as clientID Cannot be used for Azure Managed Service Identity</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tenantID</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>tenant ID of the managed identity, cannot be used at the same time as resourceID</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.CNAMEStrategy"> CNAMEStrategy (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolverDNS01">ACMEChallengeSolverDNS01</a>) </p>
<div>
  <p>CNAMEStrategy configures how the DNS01 provider should handle CNAME records when found in DNS zones. By default, the None strategy will be applied (i.e. do not follow CNAMEs).</p>
</div>
<h3 id="acme.cert-manager.io/v1.CertificateDNSNameSelector">CertificateDNSNameSelector</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</a>) </p>
<div>
  <p>CertificateDNSNameSelector selects certificates using a label selector, and can optionally select individual DNS names within those certificates. If both MatchLabels and DNSNames are empty, this selector will match all certificates and DNS names within them.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>matchLabels</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>A label selector that is used to refine the set of certificate&rsquo;s that this challenge solver will apply to.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dnsNames</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>List of DNSNames that this solver will be used to solve. If specified and a match is found, a dnsNames selector will take precedence over a dnsZones selector. If multiple solvers match with the same dnsNames value, the solver with the most matching labels in matchLabels will be selected. If neither has more matches, the solver defined earlier in the list will be selected.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dnsZones</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>List of DNSZones that this solver will be used to solve. The most specific DNS zone match specified here will take precedence over other DNS zone matches, so a solver specifying sys.example.com will be selected over one specifying example.com for the domain www.sys.example.com. If multiple solvers match with the same dnsZones value, the solver with the most matching labels in matchLabels will be selected. If neither has more matches, the solver defined earlier in the list will be selected.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ChallengeSpec">ChallengeSpec</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Challenge">Challenge</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The URL of the ACME Challenge resource for this challenge. This can be used to lookup details about the status of this challenge.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>authorizationURL</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The URL to the ACME Authorization resource that this challenge is a part of.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dnsName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> dnsName is the identifier that this challenge is for, e.g., example.com. If the requested DNSName is a &lsquo;wildcard&rsquo;, this field MUST be set to the non-wildcard domain, e.g., for <code>*.example.com</code>, it must be <code>example.com</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>wildcard</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>wildcard will be true if this challenge is for a wildcard identifier, for example &lsquo;*.example.com&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeType">ACMEChallengeType</a>
        </em>
      </td>
      <td>
        <p>The type of ACME challenge this resource represents. One of &ldquo;HTTP-01&rdquo; or &ldquo;DNS-01&rdquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>token</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The ACME challenge token for this challenge. This is the raw value returned from the ACME server.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>key</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>
          The ACME challenge key for this challenge For HTTP01 challenges, this is the value that must be responded with to complete the HTTP01 challenge in the format:
          <code>&lt;private key JWK thumbprint&gt;.&lt;key from acme server for challenge&gt;</code>. For DNS01 challenges, this is the base64 encoded SHA256 sum of the
          <code>&lt;private key JWK thumbprint&gt;.&lt;key from acme server for challenge&gt;</code>
          text that must be set as the TXT record content.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solver</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEChallengeSolver">ACMEChallengeSolver</a>
        </em>
      </td>
      <td>
        <p>Contains the domain solving configuration that should be used to solve this challenge resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuerRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
        </em>
      </td>
      <td>
        <p>References a properly configured ACME-type Issuer which should be used to create this Challenge. If the Issuer does not exist, processing will be retried. If the Issuer is not an &lsquo;ACME&rsquo; Issuer, an error will be returned and the Challenge will be marked as failed.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ChallengeStatus">ChallengeStatus</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Challenge">Challenge</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>processing</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Used to denote whether this challenge should be processed or not. This field will only be set to true by the &lsquo;scheduling&rsquo; component. It will only be set to false by the &lsquo;challenges&rsquo; controller, after the challenge has reached a final state or timed out. If this field is set to false, the challenge controller will not take any more action.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>presented</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> presented will be set to true if the challenge values for this challenge are currently &lsquo;presented&rsquo;. This <em>does not</em> imply the self check is passing. Only that the values have been &lsquo;submitted&rsquo; for the appropriate challenge mechanism (i.e. the DNS01 TXT record has been presented, or the HTTP01 configuration has been configured). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>reason</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Contains human readable information on why the Challenge is in the current state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>state</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.State">State</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Contains the current &lsquo;state&rsquo; of the challenge. If not set, the state of the challenge is unknown.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.HMACKeyAlgorithm"> HMACKeyAlgorithm (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEExternalAccountBinding">ACMEExternalAccountBinding</a>) </p>
<div>
  <p>HMACKeyAlgorithm is the name of a key algorithm used for HMAC encryption</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;HS256&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;HS384&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;HS512&#34;</p>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.OrderSpec">OrderSpec</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Order">Order</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>request</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <p>Certificate signing request bytes in DER encoding. This will be used when finalizing the order. This field must be set on the order.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuerRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
        </em>
      </td>
      <td>
        <p>IssuerRef references a properly configured ACME-type Issuer which should be used to create this Order. If the Issuer does not exist, processing will be retried. If the Issuer is not an &lsquo;ACME&rsquo; Issuer, an error will be returned and the Order will be marked as failed.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>commonName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> CommonName is the common name as specified on the DER encoded CSR. If specified, this value must also be present in <code>dnsNames</code> or <code>ipAddresses</code>. This field must match the corresponding field on the DER encoded CSR. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dnsNames</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>DNSNames is a list of DNS names that should be included as part of the Order validation process. This field must match the corresponding field on the DER encoded CSR.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ipAddresses</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>IPAddresses is a list of IP addresses that should be included as part of the Order validation process. This field must match the corresponding field on the DER encoded CSR.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>duration</code>
        <br />
        <em>
          <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Duration is the duration for the not after date for the requested certificate. this is set on order creation as pe the ACME spec.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>profile</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Profile allows requesting a certificate profile from the ACME server. Supported profiles are listed by the server&rsquo;s ACME directory URL.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.OrderStatus">OrderStatus</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Order">Order</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>URL of the Order. This will initially be empty when the resource is first created. The Order controller will populate this field when the Order is first processed. This field will be immutable after it is initially set.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>finalizeURL</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>FinalizeURL of the Order. This is used to obtain certificates for this order once it has been completed.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>authorizations</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEAuthorization">[]ACMEAuthorization</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Authorizations contains data returned from the ACME server on what authorizations must be completed in order to validate the DNS names specified on the Order.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>certificate</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Certificate is a copy of the PEM encoded certificate for this Order. This field will be populated after the order has been successfully finalized with the ACME server, and the order has transitioned to the &lsquo;valid&rsquo; state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>state</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.State">State</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>State contains the current state of this Order resource. States &lsquo;success&rsquo; and &lsquo;expired&rsquo; are &lsquo;final&rsquo;</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>reason</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reason optionally provides more information about a why the order is in the current state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>failureTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>FailureTime stores the time that this order failed. This is used to influence garbage collection and back-off.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.Route53Auth">Route53Auth</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRoute53">ACMEIssuerDNS01ProviderRoute53</a>) </p>
<div>
  <p>Route53Auth is configuration used to authenticate with a Route53.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>kubernetes</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.Route53KubernetesAuth">Route53KubernetesAuth</a>
        </em>
      </td>
      <td>
        <p>Kubernetes authenticates with Route53 using AssumeRoleWithWebIdentity by passing a bound ServiceAccount token.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.Route53KubernetesAuth">Route53KubernetesAuth</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Route53Auth">Route53Auth</a>) </p>
<div>
  <p>Route53KubernetesAuth is a configuration to authenticate against Route53 using a bound Kubernetes ServiceAccount token.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>serviceAccountRef</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ServiceAccountRef">ServiceAccountRef</a>
        </em>
      </td>
      <td>
        <p>A reference to a service account that will be used to request a bound token (also known as &ldquo;projected token&rdquo;). To use this field, you must configure an RBAC rule to let cert-manager request a token.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.ServiceAccountRef">ServiceAccountRef</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.Route53KubernetesAuth">Route53KubernetesAuth</a>) </p>
<div>
  <p>ServiceAccountRef is a service account used by cert-manager to request a token. The expiration of the token is also set by cert-manager to 10 minutes.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Name of the ServiceAccount used to request a token.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>audiences</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> TokenAudiences is an optional list of audiences to include in the token passed to AWS. The default token consisting of the issuer&rsquo;s namespace and name is always included. If unset the audience defaults to <code>sts.amazonaws.com</code>. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="acme.cert-manager.io/v1.State"> State (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEAuthorization">ACMEAuthorization</a>, <a href="#acme.cert-manager.io/v1.ChallengeStatus">ChallengeStatus</a>, <a href="#acme.cert-manager.io/v1.OrderStatus">OrderStatus</a>) </p>
<div>
  <p>
    State represents the state of an ACME resource, such as an Order. The possible options here map to the corresponding values in the ACME specification. Full details of these values can be found here: <a href="https://tools.ietf.org/html/draft-ietf-acme-acme-15#section-7.1.6">https://tools.ietf.org/html/draft-ietf-acme-acme-15#section-7.1.6</a>
    Clients utilising this type must also gracefully handle unknown values, as the contents of this enumeration may be added to over time.
  </p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;errored&#34;</p>
      </td>
      <td>
        <p>Errored signifies that the ACME resource has errored for some reason. This is a catch-all state, and is used for marking internal cert-manager errors such as validation failures. This is a final state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;expired&#34;</p>
      </td>
      <td>
        <p>Expired signifies that an ACME resource has expired. If an Order is marked &lsquo;Expired&rsquo;, one of its validations may have expired or the Order itself. This is a final state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;invalid&#34;</p>
      </td>
      <td>
        <p>Invalid signifies that an ACME resource is invalid for some reason. If an Order is marked &lsquo;invalid&rsquo;, one of its validations must be invalid for some reason. This is a final state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;pending&#34;</p>
      </td>
      <td>
        <p>Pending signifies that an ACME resource is still pending and is not yet ready. If an Order is marked &lsquo;Pending&rsquo;, the validations for that Order are still in progress. This is a transient state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;processing&#34;</p>
      </td>
      <td>
        <p>Processing signifies that an ACME resource is being processed by the server. If an Order is marked &lsquo;Processing&rsquo;, the validations for that Order are currently being processed. This is a transient state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;ready&#34;</p>
      </td>
      <td>
        <p>Ready signifies that an ACME resource is in a ready state. If an order is &lsquo;ready&rsquo;, all of its challenges have been completed successfully and the order is ready to be finalized. Once finalized, it will transition to the Valid state. This is a transient state.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;&#34;</p>
      </td>
      <td>
        <p>Unknown is not a real state as part of the ACME spec. It is used to represent an unrecognised value.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;valid&#34;</p>
      </td>
      <td>
        <p>Valid signifies that an ACME resource is in a valid state. If an order is &lsquo;valid&rsquo;, it has been finalized with the ACME server and the certificate can be retrieved from the ACME server using the certificate URL stored in the Order&rsquo;s status subresource. This is a final state.</p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<h2 id="cainjector.config.cert-manager.io/v1alpha1">cainjector.config.cert-manager.io/v1alpha1</h2>
<div>
  <p>Package v1alpha1 is the v1alpha1 version of the cainjector config API.</p>
</div>
<p>Resource Types:</p>
<ul></ul>
<h3 id="cainjector.config.cert-manager.io/v1alpha1.CAInjectorConfiguration">CAInjectorConfiguration</h3>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>kubeConfig</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>kubeConfig is the kubeconfig file used to connect to the Kubernetes apiserver. If not specified, the cainjector will attempt to load the in-cluster-config.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>namespace</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>If set, this limits the scope of cainjector to a single namespace. If set, cainjector will not update resources with certificates outside of the configured namespace.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>leaderElectionConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.LeaderElectionConfig</em>
      </td>
      <td>
        <p>LeaderElectionConfig configures the behaviour of the leader election</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enableDataSourceConfig</code>
        <br />
        <em>
          <a href="#cainjector.config.cert-manager.io/v1alpha1.EnableDataSourceConfig">EnableDataSourceConfig</a>
        </em>
      </td>
      <td>
        <p>EnableDataSourceConfig determines whether cainjector&rsquo;s control loops will watch cert-manager resources as potential sources of CA data.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enableInjectableConfig</code>
        <br />
        <em>
          <a href="#cainjector.config.cert-manager.io/v1alpha1.EnableInjectableConfig">EnableInjectableConfig</a>
        </em>
      </td>
      <td>
        <p>EnableInjectableConfig determines whether cainjector&rsquo;s control loops will watch cert-manager resources as potential targets for CA data injection.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enablePprof</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Enable profiling for cainjector.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>pprofAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port that Go profiler should listen on, i.e localhost:6060. Ensure that profiler is not exposed on a public address. Profiler will be served at /debug/pprof.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>logging</code>
        <br />
        <em>k8s.io/component-base/logs/api/v1.LoggingConfiguration</em>
      </td>
      <td>
        <p>
          logging configures the logging behaviour of the cainjector.
          <a href="https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration">https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration</a>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>featureGates</code>
        <br />
        <em>map[string]bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>featureGates is a map of feature names to bools that enable or disable experimental features.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsListenAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port that the metrics endpoint should listen on. The value &ldquo;0&rdquo; disables the metrics server. Defaults to &lsquo;0.0.0.0:9402&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsTLSConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.TLSConfig</em>
      </td>
      <td>
        <p>metricsTLSConfig is used to configure the metrics server TLS settings.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cainjector.config.cert-manager.io/v1alpha1.EnableDataSourceConfig">EnableDataSourceConfig</h3>
<p> (<em>Appears on:</em> <a href="#cainjector.config.cert-manager.io/v1alpha1.CAInjectorConfiguration">CAInjectorConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>certificates</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Certificates determines whether cainjector&rsquo;s control loops will watch cert-manager Certificate resources as potential sources of CA data. If not set, defaults to true.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cainjector.config.cert-manager.io/v1alpha1.EnableInjectableConfig">EnableInjectableConfig</h3>
<p> (<em>Appears on:</em> <a href="#cainjector.config.cert-manager.io/v1alpha1.CAInjectorConfiguration">CAInjectorConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>validatingWebhookConfigurations</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>ValidatingWebhookConfigurations determines whether cainjector will spin up a control loop to inject CA data to annotated ValidatingWebhookConfigurations If not set, defaults to true.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>mutatingWebhookConfigurations</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>MutatingWebhookConfigurations determines whether cainjector will spin up a control loop to inject CA data to annotated MutatingWebhookConfigurations If not set, defaults to true.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>customResourceDefinitions</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>CustomResourceDefinitions determines whether cainjector will spin up a control loop to inject CA data to annotated CustomResourceDefinitions If not set, defaults to true.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiServices</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>APIServices determines whether cainjector will spin up a control loop to inject CA data to annotated APIServices If not set, defaults to true.</p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<h2 id="cert-manager.io/v1">cert-manager.io/v1</h2>
<div>
  <p>Package v1 is the v1 version of the API.</p>
</div>
<p>Resource Types:</p>
<ul>
  <li>
    <a href="#cert-manager.io/v1.Certificate">Certificate</a>
  </li>
  <li>
    <a href="#cert-manager.io/v1.CertificateRequest">CertificateRequest</a>
  </li>
  <li>
    <a href="#cert-manager.io/v1.ClusterIssuer">ClusterIssuer</a>
  </li>
  <li>
    <a href="#cert-manager.io/v1.Issuer">Issuer</a>
  </li>
</ul>
<h3 id="cert-manager.io/v1.Certificate">Certificate</h3>
<div>
  <p> A Certificate resource should be created to ensure an up to date and signed X.509 certificate is stored in the Kubernetes Secret resource named in <code>spec.secretName</code>. </p>
  <p> The stored certificate will be renewed before it expires (as configured by <code>spec.renewBefore</code>). </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>Certificate</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Standard object&rsquo;s metadata. More info: <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata</a> </p>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          Specification of the desired state of the Certificate resource.
          <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status</a>
        </p>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>subject</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.X509Subject">X509Subject</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> Requested set of X509 certificate subject attributes. More info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6">https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6</a> </p>
              <p> The common name attribute is specified separately in the <code>commonName</code> field. Cannot be set if the <code>literalSubject</code> field is set. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>literalSubject</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> Requested X.509 certificate subject, represented using the LDAP &ldquo;String Representation of a Distinguished Name&rdquo; [1]. Important: the LDAP string format also specifies the order of the attributes in the subject, this is important when issuing certs for LDAP authentication. Example: <code>CN=foo,DC=corp,DC=example,DC=com</code> More info [1]: <a href="https://datatracker.ietf.org/doc/html/rfc4514">https://datatracker.ietf.org/doc/html/rfc4514</a> More info: <a href="https://github.com/cert-manager/cert-manager/issues/3203">https://github.com/cert-manager/cert-manager/issues/3203</a> More info: <a href="https://github.com/cert-manager/cert-manager/issues/4424">https://github.com/cert-manager/cert-manager/issues/4424</a> </p>
              <p> Cannot be set if the <code>subject</code> or <code>commonName</code> field is set. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>commonName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> Requested common name X509 certificate subject attribute. More info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6">https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6</a> NOTE: TLS clients will ignore this value when any subject alternative name is set (see <a href="https://tools.ietf.org/html/rfc6125#section-6.4.4">https://tools.ietf.org/html/rfc6125#section-6.4.4</a>). </p>
              <p> Should have a length of 64 characters or fewer to avoid generating invalid CSRs. Cannot be set if the <code>literalSubject</code> field is set. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>duration</code>
              <br />
              <em>
                <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested &lsquo;duration&rsquo; (i.e. lifetime) of the Certificate. Note that the issuer may choose to ignore the requested duration, just like any other requested attribute.</p>
              <p> If unset, this defaults to 90 days. Minimum accepted duration is 1 hour. Value must be in units accepted by Go time.ParseDuration <a href="https://golang.org/pkg/time/#ParseDuration">https://golang.org/pkg/time/#ParseDuration</a>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>renewBefore</code>
              <br />
              <em>
                <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> How long before the currently issued certificate&rsquo;s expiry cert-manager should renew the certificate. For example, if a certificate is valid for 60 minutes, and <code>renewBefore=10m</code>, cert-manager will begin to attempt to renew the certificate 50 minutes after it was issued (i.e. when there are 10 minutes remaining until the certificate is no longer valid). </p>
              <p>NOTE: The actual lifetime of the issued certificate is used to determine the renewal time. If an issuer returns a certificate with a different lifetime than the one requested, cert-manager will use the lifetime of the issued certificate.</p>
              <p> If unset, this defaults to <sup>1</sup>&frasl;<sub>3</sub> of the issued certificate&rsquo;s lifetime. Minimum accepted value is 5 minutes. Value must be in units accepted by Go time.ParseDuration <a href="https://golang.org/pkg/time/#ParseDuration">https://golang.org/pkg/time/#ParseDuration</a>. Cannot be set if the <code>renewBeforePercentage</code> field is set. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>renewBeforePercentage</code>
              <br />
              <em>int32</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> <code>renewBeforePercentage</code> is like <code>renewBefore</code>, except it is a relative percentage rather than an absolute duration. For example, if a certificate is valid for 60 minutes, and <code>renewBeforePercentage=25</code>, cert-manager will begin to attempt to renew the certificate 45 minutes after it was issued (i.e. when there are 15 minutes (25%) remaining until the certificate is no longer valid). </p>
              <p>NOTE: The actual lifetime of the issued certificate is used to determine the renewal time. If an issuer returns a certificate with a different lifetime than the one requested, cert-manager will use the lifetime of the issued certificate.</p>
              <p>
                Value must be an integer in the range (0,100). The minimum effective
                <code>renewBefore</code> derived from the <code>renewBeforePercentage</code> and <code>duration</code> fields is 5 minutes. Cannot be set if the <code>renewBefore</code> field is set.
              </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>dnsNames</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested DNS subject alternative names.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>ipAddresses</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested IP address subject alternative names.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>uris</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested URI subject alternative names.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>otherNames</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.OtherName">[]OtherName</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> <code>otherNames</code> is an escape hatch for SAN that allows any type. We currently restrict the support to string like otherNames, cf RFC 5280 p 37 Any UTF8 String valued otherName can be passed with by setting the keys oid: x.x.x.x and UTF8Value: somevalue for <code>otherName</code>. Most commonly this would be UPN set with oid: 1.3.6.1.4.1.311.20.2.3 You should ensure that any OID passed is valid for the UTF8String type as we do not explicitly validate this. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>emailAddresses</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested email subject alternative names.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>secretName</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <p>Name of the Secret resource that will be automatically created and managed by this Certificate resource. It will be populated with a private key and certificate, signed by the denoted issuer. The Secret resource lives in the same namespace as the Certificate resource.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>secretTemplate</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.CertificateSecretTemplate">CertificateSecretTemplate</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Defines annotations and labels to be copied to the Certificate&rsquo;s Secret. Labels and annotations on the Secret will be changed as they appear on the SecretTemplate when added or removed. SecretTemplate annotations are added in conjunction with, and cannot overwrite, the base set of annotations cert-manager sets on the Certificate&rsquo;s Secret.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>keystores</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.CertificateKeystores">CertificateKeystores</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Additional keystore output formats to be stored in the Certificate&rsquo;s Secret.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>issuerRef</code>
              <br />
              <em>
                <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
              </em>
            </td>
            <td>
              <p>Reference to the issuer responsible for issuing the certificate. If the issuer is namespace-scoped, it must be in the same namespace as the Certificate. If the issuer is cluster-scoped, it can be used from any namespace.</p>
              <p> The <code>name</code> field of the reference must always be specified. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>isCA</code>
              <br />
              <em>bool</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> Requested basic constraints isCA value. The isCA value is used to set the <code>isCA</code> field on the created CertificateRequest resources. Note that the issuer may choose to ignore the requested isCA value, just like any other requested attribute. </p>
              <p> If true, this will automatically add the <code>cert sign</code> usage to the list of requested <code>usages</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>usages</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.KeyUsage">[]KeyUsage</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> Requested key usages and extended key usages. These usages are used to set the <code>usages</code> field on the created CertificateRequest resources. If <code>encodeUsagesInRequest</code> is unset or set to <code>true</code>, the usages will additionally be encoded in the <code>request</code> field which contains the CSR blob. </p>
              <p> If unset, defaults to <code>digital signature</code> and <code>key encipherment</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>privateKey</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Private key options. These include the key algorithm and size, the used encoding and the rotation policy.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>signatureAlgorithm</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.SignatureAlgorithm">SignatureAlgorithm</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Signature algorithm to use. Allowed values for RSA keys: SHA256WithRSA, SHA384WithRSA, SHA512WithRSA. Allowed values for ECDSA keys: ECDSAWithSHA256, ECDSAWithSHA384, ECDSAWithSHA512. Allowed values for Ed25519 keys: PureEd25519.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>encodeUsagesInRequest</code>
              <br />
              <em>bool</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Whether the KeyUsage and ExtKeyUsage extensions should be set in the encoded CSR.</p>
              <p>This option defaults to true, and should only be disabled if the target issuer does not support CSRs with these X509 KeyUsage/ ExtKeyUsage extensions.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>revisionHistoryLimit</code>
              <br />
              <em>int32</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>
                The maximum number of CertificateRequest revisions that are maintained in the Certificate&rsquo;s history. Each revision represents a single <code>CertificateRequest</code>
                created by this Certificate, either when it was created, renewed, or Spec was changed. Revisions will be removed by oldest first if the number of revisions exceeds this number.
              </p>
              <p> If set, revisionHistoryLimit must be a value of <code>1</code> or greater. Default value is <code>1</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>additionalOutputFormats</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.CertificateAdditionalOutputFormat">[]CertificateAdditionalOutputFormat</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Defines extra output formats of the private key and signed certificate chain to be written to this Certificate&rsquo;s target Secret.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>nameConstraints</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.NameConstraints">NameConstraints</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p> x.509 certificate NameConstraint extension which MUST NOT be used in a non-CA certificate. More Info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.2.1.10">https://datatracker.ietf.org/doc/html/rfc5280#section-4.2.1.10</a> </p>
              <p>
                This is an Alpha Feature and is only enabled with the
                <code>--feature-gates=NameConstraints=true</code> option set on both the controller and webhook components.
              </p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateStatus">CertificateStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Status of the Certificate. This is set and managed automatically. Read-only. More info: <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status</a> </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateRequest">CertificateRequest</h3>
<div>
  <p>A CertificateRequest is used to request a signed certificate from one of the configured issuers.</p>
  <p> All fields within the CertificateRequest&rsquo;s <code>spec</code> are immutable after creation. A CertificateRequest will either succeed or fail, as denoted by its <code>Ready</code> status condition and its <code>status.failureTime</code> field. </p>
  <p>A CertificateRequest is a one-shot resource, meaning it represents a single point in time request for a certificate and cannot be re-used.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>CertificateRequest</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Standard object&rsquo;s metadata. More info: <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata</a> </p>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateRequestSpec">CertificateRequestSpec</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          Specification of the desired state of the CertificateRequest resource.
          <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status</a>
        </p>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>duration</code>
              <br />
              <em>
                <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested &lsquo;duration&rsquo; (i.e. lifetime) of the Certificate. Note that the issuer may choose to ignore the requested duration, just like any other requested attribute.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>issuerRef</code>
              <br />
              <em>
                <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
              </em>
            </td>
            <td>
              <p>Reference to the issuer responsible for issuing the certificate. If the issuer is namespace-scoped, it must be in the same namespace as the Certificate. If the issuer is cluster-scoped, it can be used from any namespace.</p>
              <p> The <code>name</code> field of the reference must always be specified. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>request</code>
              <br />
              <em>[]byte</em>
            </td>
            <td>
              <p>The PEM-encoded X.509 certificate signing request to be submitted to the issuer for signing.</p>
              <p> If the CSR has a BasicConstraints extension, its isCA attribute must match the <code>isCA</code> value of this CertificateRequest. If the CSR has a KeyUsage extension, its key usages must match the key usages in the <code>usages</code> field of this CertificateRequest. If the CSR has a ExtKeyUsage extension, its extended key usages must match the extended key usages in the <code>usages</code> field of this CertificateRequest. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>isCA</code>
              <br />
              <em>bool</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested basic constraints isCA value. Note that the issuer may choose to ignore the requested isCA value, just like any other requested attribute.</p>
              <p> NOTE: If the CSR in the <code>Request</code> field has a BasicConstraints extension, it must have the same isCA value as specified here. </p>
              <p> If true, this will automatically add the <code>cert sign</code> usage to the list of requested <code>usages</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>usages</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.KeyUsage">[]KeyUsage</a>
              </em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Requested key usages and extended key usages.</p>
              <p> NOTE: If the CSR in the <code>Request</code> field has uses the KeyUsage or ExtKeyUsage extension, these extensions must have the same values as specified here without any additional values. </p>
              <p> If unset, defaults to <code>digital signature</code> and <code>key encipherment</code>. </p>
            </td>
          </tr>
          <tr>
            <td>
              <code>username</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Username contains the name of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>uid</code>
              <br />
              <em>string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>UID contains the uid of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>groups</code>
              <br />
              <em>[]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Groups contains group membership of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
            </td>
          </tr>
          <tr>
            <td>
              <code>extra</code>
              <br />
              <em>map[string][]string</em>
            </td>
            <td>
              <em>(Optional)</em>
              <p>Extra contains extra attributes of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateRequestStatus">CertificateRequestStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Status of the CertificateRequest. This is set and managed automatically. Read-only. More info: <a href="https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status">https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status</a> </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.ClusterIssuer">ClusterIssuer</h3>
<div>
  <p> A ClusterIssuer represents a certificate issuing authority which can be referenced as part of <code>issuerRef</code> fields. It is similar to an Issuer, however it is cluster-scoped and therefore can be referenced by resources that exist in <em>any</em> namespace, not just the same namespace as the referent. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>ClusterIssuer</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerSpec">IssuerSpec</a>
        </em>
      </td>
      <td>
        <p>Desired state of the ClusterIssuer resource.</p>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>IssuerConfig</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>
              </em>
            </td>
            <td>
              <p> (Members of <code>IssuerConfig</code> are embedded into this type.) </p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerStatus">IssuerStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Status of the ClusterIssuer. This is set and managed automatically.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.Issuer">Issuer</h3>
<div>
  <p> An Issuer represents a certificate issuing authority which can be referenced as part of <code>issuerRef</code> fields. It is scoped to a single namespace and can therefore only be referenced by resources within the same namespace. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>apiVersion</code>
        <br />
        string
      </td>
      <td>
        <code>cert-manager.io/v1</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        string
      </td>
      <td>
        <code>Issuer</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>metadata</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#objectmeta-v1-meta">Kubernetes meta/v1.ObjectMeta</a>
        </em>
      </td>
      <td>
        Refer to the Kubernetes API documentation for the fields of the
        <code>metadata</code> field.
      </td>
    </tr>
    <tr>
      <td>
        <code>spec</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerSpec">IssuerSpec</a>
        </em>
      </td>
      <td>
        <p>Desired state of the Issuer resource.</p>
        <br />
        <br />
        <table>
          <tr>
            <td>
              <code>IssuerConfig</code>
              <br />
              <em>
                <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>
              </em>
            </td>
            <td>
              <p> (Members of <code>IssuerConfig</code> are embedded into this type.) </p>
            </td>
          </tr>
        </table>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerStatus">IssuerStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Status of the Issuer. This is set and managed automatically.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CAIssuer">CAIssuer</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>secretName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>SecretName is the name of the secret used to sign Certificates issued by this Issuer.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>crlDistributionPoints</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The CRL distribution points is an X.509 v3 certificate extension which identifies the location of the CRL from which the revocation of this certificate can be checked. If not set, certificates will be issued without distribution points set.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ocspServers</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The OCSP server list is an X.509 v3 extension that defines a list of URLs of OCSP responders. The OCSP responders can be queried for the revocation status of an issued certificate. If not set, the certificate will be issued with no OCSP servers set. For example, an OCSP server URL could be &ldquo;<a href='http://ocsp.int-x3.letsencrypt.org"'>http://ocsp.int-x3.letsencrypt.org&rdquo;</a>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuingCertificateURLs</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> IssuingCertificateURLs is a list of URLs which this issuer should embed into certificates it creates. See <a href="https://www.rfc-editor.org/rfc/rfc5280#section-4.2.2.1">https://www.rfc-editor.org/rfc/rfc5280#section-4.2.2.1</a> for more details. As an example, such a URL might be &ldquo;<a href='http://ca.domain.com/ca.crt"'>http://ca.domain.com/ca.crt&rdquo;</a>. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateAdditionalOutputFormat">CertificateAdditionalOutputFormat</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>CertificateAdditionalOutputFormat defines an additional output format of a Certificate resource. These contain supplementary data formats of the signed certificate chain and paired private key.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateOutputFormatType">CertificateOutputFormatType</a>
        </em>
      </td>
      <td>
        <p>Type is the name of the format type that should be written to the Certificate&rsquo;s target Secret.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateCondition">CertificateCondition</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateStatus">CertificateStatus</a>) </p>
<div>
  <p>CertificateCondition contains condition information for a Certificate.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateConditionType">CertificateConditionType</a>
        </em>
      </td>
      <td>
        <p> Type of the condition, known values are (<code>Ready</code>, <code>Issuing</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ConditionStatus">ConditionStatus</a>
        </em>
      </td>
      <td>
        <p> Status of the condition, one of (<code>True</code>, <code>False</code>, <code>Unknown</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastTransitionTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastTransitionTime is the timestamp corresponding to the last status change of this condition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>reason</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reason is a brief machine readable explanation for the condition&rsquo;s last transition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>message</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Message is a human readable description of the details of the last transition, complementing reason.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>observedGeneration</code>
        <br />
        <em>int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If set, this represents the .metadata.generation that the condition was set based upon. For instance, if .metadata.generation is currently 12, but the .status.condition[x].observedGeneration is 9, the condition is out of date with respect to the current state of the Certificate.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateConditionType"> CertificateConditionType (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateCondition">CertificateCondition</a>) </p>
<div>
  <p>CertificateConditionType represents a Certificate condition value.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;Issuing&#34;</p>
      </td>
      <td>
        <p>
          A condition added to Certificate resources when an issuance is required. This condition will be automatically added and set to true if: * No keypair data exists in the target Secret * The data stored in the Secret cannot be decoded * The private key and certificate do not have matching public keys * If a CertificateRequest for the current revision exists and the certificate data stored in the Secret does not match the
          <code>status.certificate</code> on the CertificateRequest. * If no CertificateRequest resource exists for the current revision, the options on the Certificate resource are compared against the X.509 data in the Secret, similar to what&rsquo;s done in earlier versions. If there is a mismatch, an issuance is triggered. This condition may also be added by external API consumers to trigger a re-issuance manually for any other reason.
        </p>
        <p>It will be removed by the &lsquo;issuing&rsquo; controller upon completing issuance.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Ready&#34;</p>
      </td>
      <td>
        <p>CertificateConditionReady indicates that a certificate is ready for use. This is defined as: - The target secret exists - The target secret contains a certificate that has not expired - The target secret contains a private key valid for the certificate - The commonName and dnsNames attributes match those specified on the Certificate</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateKeystores">CertificateKeystores</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>CertificateKeystores configures additional keystore output formats to be created in the Certificate&rsquo;s output Secret.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>jks</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.JKSKeystore">JKSKeystore</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          JKS configures options for storing a JKS keystore in the
          <code>spec.secretName</code> Secret resource.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>pkcs12</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.PKCS12Keystore">PKCS12Keystore</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          PKCS12 configures options for storing a PKCS12 keystore in the
          <code>spec.secretName</code> Secret resource.
        </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateOutputFormatType"> CertificateOutputFormatType (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateAdditionalOutputFormat">CertificateAdditionalOutputFormat</a>) </p>
<div>
  <p>
    CertificateOutputFormatType specifies which additional output formats should be written to the Certificate&rsquo;s target Secret. Allowed values are <code>DER</code> or <code>CombinedPEM</code>. When Type is set to <code>DER</code> an additional entry <code>key.der</code> will be written to the Secret, containing the binary format of the private key. When Type is set to <code>CombinedPEM</code> an additional entry <code>tls-combined.pem</code>
    will be written to the Secret, containing the PEM formatted private key and signed certificate chain (tls.key + tls.crt concatenated).
  </p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;CombinedPEM&#34;</p>
      </td>
      <td>
        <p>
          CertificateOutputFormatCombinedPEM writes the Certificate&rsquo;s signed certificate chain and private key, in PEM format, to the
          <code>tls-combined.pem</code> target Secret Data key. The value at this key will include the private key PEM document, followed by at least one new line character, followed by the chain of signed certificate PEM documents (<code>&lt;private key&gt; + \n + &lt;signed certificate chain&gt;</code>).
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;DER&#34;</p>
      </td>
      <td>
        <p> CertificateOutputFormatDER writes the Certificate&rsquo;s private key in DER binary format to the <code>key.der</code> target Secret Data key. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>CertificatePrivateKey contains configuration options for private keys used by the Certificate controller. These include the key algorithm and size, the used encoding and the rotation policy.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>rotationPolicy</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.PrivateKeyRotationPolicy">PrivateKeyRotationPolicy</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>RotationPolicy controls how private keys should be regenerated when a re-issuance is being processed.</p>
        <p> If set to <code>Never</code>, a private key will only be generated if one does not already exist in the target <code>spec.secretName</code>. If one does exist but it does not have the correct algorithm or size, a warning will be raised to await user intervention. If set to <code>Always</code>, a private key matching the specified requirements will be generated whenever a re-issuance occurs. Default is <code>Always</code>. The default was changed from <code>Never</code> to <code>Always</code> in cert-manager &gt;=v1.18.0. The new default can be disabled by setting the <code>--feature-gates=DefaultPrivateKeyRotationPolicyAlways=false</code> option on the controller component. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>encoding</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.PrivateKeyEncoding">PrivateKeyEncoding</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The private key cryptography standards (PKCS) encoding for this certificate&rsquo;s private key to be encoded in.</p>
        <p> If provided, allowed values are <code>PKCS1</code> and <code>PKCS8</code> standing for PKCS#1 and PKCS#8, respectively. Defaults to <code>PKCS1</code> if not specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>algorithm</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.PrivateKeyAlgorithm">PrivateKeyAlgorithm</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Algorithm is the private key algorithm of the corresponding private key for this certificate.</p>
        <p> If provided, allowed values are either <code>RSA</code>, <code>ECDSA</code> or <code>Ed25519</code>. If <code>algorithm</code> is specified and <code>size</code> is not provided, key size of 2048 will be used for <code>RSA</code> key algorithm and key size of 256 will be used for <code>ECDSA</code> key algorithm. key size is ignored when using the <code>Ed25519</code> key algorithm. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>size</code>
        <br />
        <em>int</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Size is the key bit size of the corresponding private key for this certificate.</p>
        <p> If <code>algorithm</code> is set to <code>RSA</code>, valid values are <code>2048</code>, <code>4096</code> or <code>8192</code>, and will default to <code>2048</code> if not specified. If <code>algorithm</code> is set to <code>ECDSA</code>, valid values are <code>256</code>, <code>384</code> or <code>521</code>, and will default to <code>256</code> if not specified. If <code>algorithm</code> is set to <code>Ed25519</code>, Size is ignored. No other values are allowed. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateRequestCondition">CertificateRequestCondition</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateRequestStatus">CertificateRequestStatus</a>) </p>
<div>
  <p>CertificateRequestCondition contains condition information for a CertificateRequest.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateRequestConditionType">CertificateRequestConditionType</a>
        </em>
      </td>
      <td>
        <p> Type of the condition, known values are (<code>Ready</code>, <code>InvalidRequest</code>,<code>Approved</code>, <code>Denied</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ConditionStatus">ConditionStatus</a>
        </em>
      </td>
      <td>
        <p> Status of the condition, one of (<code>True</code>, <code>False</code>, <code>Unknown</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastTransitionTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastTransitionTime is the timestamp corresponding to the last status change of this condition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>reason</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reason is a brief machine readable explanation for the condition&rsquo;s last transition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>message</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Message is a human readable description of the details of the last transition, complementing reason.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateRequestConditionType"> CertificateRequestConditionType (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateRequestCondition">CertificateRequestCondition</a>) </p>
<div>
  <p>CertificateRequestConditionType represents a Certificate condition value.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;Approved&#34;</p>
      </td>
      <td>
        <p>
          CertificateRequestConditionApproved indicates that a certificate request is approved and ready for signing. Condition must never have a status of
          <code>False</code>, and cannot be modified once set. Cannot be set alongside <code>Denied</code>.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Denied&#34;</p>
      </td>
      <td>
        <p>
          CertificateRequestConditionDenied indicates that a certificate request is denied, and must never be signed. Condition must never have a status of
          <code>False</code>, and cannot be modified once set. Cannot be set alongside <code>Approved</code>.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;InvalidRequest&#34;</p>
      </td>
      <td>
        <p> CertificateRequestConditionInvalidRequest indicates that a certificate signer has refused to sign the request due to at least one of the input parameters being invalid. Additional information about why the request was rejected can be found in the <code>reason</code> and <code>message</code> fields. </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Ready&#34;</p>
      </td>
      <td>
        <p>CertificateRequestConditionReady indicates that a certificate is ready for use. This is defined as: - The target certificate exists in CertificateRequest.Status</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateRequestSpec">CertificateRequestSpec</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateRequest">CertificateRequest</a>) </p>
<div>
  <p>CertificateRequestSpec defines the desired state of CertificateRequest</p>
  <p>NOTE: It is important to note that the issuer can choose to ignore or change any of the requested attributes. How the issuer maps a certificate request to a signed certificate is the full responsibility of the issuer itself. For example, as an edge case, an issuer that inverts the isCA value is free to do so.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>duration</code>
        <br />
        <em>
          <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested &lsquo;duration&rsquo; (i.e. lifetime) of the Certificate. Note that the issuer may choose to ignore the requested duration, just like any other requested attribute.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuerRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
        </em>
      </td>
      <td>
        <p>Reference to the issuer responsible for issuing the certificate. If the issuer is namespace-scoped, it must be in the same namespace as the Certificate. If the issuer is cluster-scoped, it can be used from any namespace.</p>
        <p> The <code>name</code> field of the reference must always be specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>request</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <p>The PEM-encoded X.509 certificate signing request to be submitted to the issuer for signing.</p>
        <p> If the CSR has a BasicConstraints extension, its isCA attribute must match the <code>isCA</code> value of this CertificateRequest. If the CSR has a KeyUsage extension, its key usages must match the key usages in the <code>usages</code> field of this CertificateRequest. If the CSR has a ExtKeyUsage extension, its extended key usages must match the extended key usages in the <code>usages</code> field of this CertificateRequest. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>isCA</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested basic constraints isCA value. Note that the issuer may choose to ignore the requested isCA value, just like any other requested attribute.</p>
        <p> NOTE: If the CSR in the <code>Request</code> field has a BasicConstraints extension, it must have the same isCA value as specified here. </p>
        <p> If true, this will automatically add the <code>cert sign</code> usage to the list of requested <code>usages</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>usages</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.KeyUsage">[]KeyUsage</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested key usages and extended key usages.</p>
        <p> NOTE: If the CSR in the <code>Request</code> field has uses the KeyUsage or ExtKeyUsage extension, these extensions must have the same values as specified here without any additional values. </p>
        <p> If unset, defaults to <code>digital signature</code> and <code>key encipherment</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>username</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Username contains the name of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>uid</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>UID contains the uid of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>groups</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Groups contains group membership of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>extra</code>
        <br />
        <em>map[string][]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Extra contains extra attributes of the user that created the CertificateRequest. Populated by the cert-manager webhook on creation and immutable.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateRequestStatus">CertificateRequestStatus</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateRequest">CertificateRequest</a>) </p>
<div>
  <p>CertificateRequestStatus defines the observed state of CertificateRequest and resulting signed certificate.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>conditions</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateRequestCondition">[]CertificateRequestCondition</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> List of status conditions to indicate the status of a CertificateRequest. Known condition types are <code>Ready</code>, <code>InvalidRequest</code>, <code>Approved</code> and <code>Denied</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>certificate</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          The PEM encoded X.509 certificate resulting from the certificate signing request. If not set, the CertificateRequest has either not been completed or has failed. More information on failure can be found by checking the
          <code>conditions</code> field.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ca</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The PEM encoded X.509 certificate of the signer, also known as the CA (Certificate Authority). This is set on a best-effort basis by different issuers. If not set, the CA is assumed to be unknown/not available.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>failureTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>FailureTime stores the time that this CertificateRequest failed. This is used to influence garbage collection and back-off.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateSecretTemplate">CertificateSecretTemplate</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p> CertificateSecretTemplate defines the default labels and annotations to be copied to the Kubernetes Secret resource named in <code>CertificateSpec.secretName</code>. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>annotations</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Annotations is a key value map to be copied to the target Kubernetes Secret.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>labels</code>
        <br />
        <em>map[string]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Labels is a key value map to be copied to the target Kubernetes Secret.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateSpec">CertificateSpec</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.Certificate">Certificate</a>) </p>
<div>
  <p>CertificateSpec defines the desired state of Certificate.</p>
  <p>NOTE: The specification contains a lot of &ldquo;requested&rdquo; certificate attributes, it is important to note that the issuer can choose to ignore or change any of these requested attributes. How the issuer maps a certificate request to a signed certificate is the full responsibility of the issuer itself. For example, as an edge case, an issuer that inverts the isCA value is free to do so.</p>
  <p>A valid Certificate requires at least one of a CommonName, LiteralSubject, DNSName, or URI to be valid.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>subject</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.X509Subject">X509Subject</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Requested set of X509 certificate subject attributes. More info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6">https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6</a> </p>
        <p> The common name attribute is specified separately in the <code>commonName</code> field. Cannot be set if the <code>literalSubject</code> field is set. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>literalSubject</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Requested X.509 certificate subject, represented using the LDAP &ldquo;String Representation of a Distinguished Name&rdquo; [1]. Important: the LDAP string format also specifies the order of the attributes in the subject, this is important when issuing certs for LDAP authentication. Example: <code>CN=foo,DC=corp,DC=example,DC=com</code> More info [1]: <a href="https://datatracker.ietf.org/doc/html/rfc4514">https://datatracker.ietf.org/doc/html/rfc4514</a> More info: <a href="https://github.com/cert-manager/cert-manager/issues/3203">https://github.com/cert-manager/cert-manager/issues/3203</a> More info: <a href="https://github.com/cert-manager/cert-manager/issues/4424">https://github.com/cert-manager/cert-manager/issues/4424</a> </p>
        <p> Cannot be set if the <code>subject</code> or <code>commonName</code> field is set. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>commonName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Requested common name X509 certificate subject attribute. More info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6">https://datatracker.ietf.org/doc/html/rfc5280#section-4.1.2.6</a> NOTE: TLS clients will ignore this value when any subject alternative name is set (see <a href="https://tools.ietf.org/html/rfc6125#section-6.4.4">https://tools.ietf.org/html/rfc6125#section-6.4.4</a>). </p>
        <p> Should have a length of 64 characters or fewer to avoid generating invalid CSRs. Cannot be set if the <code>literalSubject</code> field is set. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>duration</code>
        <br />
        <em>
          <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested &lsquo;duration&rsquo; (i.e. lifetime) of the Certificate. Note that the issuer may choose to ignore the requested duration, just like any other requested attribute.</p>
        <p> If unset, this defaults to 90 days. Minimum accepted duration is 1 hour. Value must be in units accepted by Go time.ParseDuration <a href="https://golang.org/pkg/time/#ParseDuration">https://golang.org/pkg/time/#ParseDuration</a>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>renewBefore</code>
        <br />
        <em>
          <a href="https://godoc.org/k8s.io/apimachinery/pkg/apis/meta/v1#Duration">Kubernetes meta/v1.Duration</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> How long before the currently issued certificate&rsquo;s expiry cert-manager should renew the certificate. For example, if a certificate is valid for 60 minutes, and <code>renewBefore=10m</code>, cert-manager will begin to attempt to renew the certificate 50 minutes after it was issued (i.e. when there are 10 minutes remaining until the certificate is no longer valid). </p>
        <p>NOTE: The actual lifetime of the issued certificate is used to determine the renewal time. If an issuer returns a certificate with a different lifetime than the one requested, cert-manager will use the lifetime of the issued certificate.</p>
        <p> If unset, this defaults to <sup>1</sup>&frasl;<sub>3</sub> of the issued certificate&rsquo;s lifetime. Minimum accepted value is 5 minutes. Value must be in units accepted by Go time.ParseDuration <a href="https://golang.org/pkg/time/#ParseDuration">https://golang.org/pkg/time/#ParseDuration</a>. Cannot be set if the <code>renewBeforePercentage</code> field is set. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>renewBeforePercentage</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> <code>renewBeforePercentage</code> is like <code>renewBefore</code>, except it is a relative percentage rather than an absolute duration. For example, if a certificate is valid for 60 minutes, and <code>renewBeforePercentage=25</code>, cert-manager will begin to attempt to renew the certificate 45 minutes after it was issued (i.e. when there are 15 minutes (25%) remaining until the certificate is no longer valid). </p>
        <p>NOTE: The actual lifetime of the issued certificate is used to determine the renewal time. If an issuer returns a certificate with a different lifetime than the one requested, cert-manager will use the lifetime of the issued certificate.</p>
        <p>
          Value must be an integer in the range (0,100). The minimum effective
          <code>renewBefore</code> derived from the <code>renewBeforePercentage</code> and <code>duration</code> fields is 5 minutes. Cannot be set if the <code>renewBefore</code> field is set.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>dnsNames</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested DNS subject alternative names.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ipAddresses</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested IP address subject alternative names.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>uris</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested URI subject alternative names.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>otherNames</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.OtherName">[]OtherName</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> <code>otherNames</code> is an escape hatch for SAN that allows any type. We currently restrict the support to string like otherNames, cf RFC 5280 p 37 Any UTF8 String valued otherName can be passed with by setting the keys oid: x.x.x.x and UTF8Value: somevalue for <code>otherName</code>. Most commonly this would be UPN set with oid: 1.3.6.1.4.1.311.20.2.3 You should ensure that any OID passed is valid for the UTF8String type as we do not explicitly validate this. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>emailAddresses</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Requested email subject alternative names.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Name of the Secret resource that will be automatically created and managed by this Certificate resource. It will be populated with a private key and certificate, signed by the denoted issuer. The Secret resource lives in the same namespace as the Certificate resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretTemplate</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateSecretTemplate">CertificateSecretTemplate</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Defines annotations and labels to be copied to the Certificate&rsquo;s Secret. Labels and annotations on the Secret will be changed as they appear on the SecretTemplate when added or removed. SecretTemplate annotations are added in conjunction with, and cannot overwrite, the base set of annotations cert-manager sets on the Certificate&rsquo;s Secret.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>keystores</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateKeystores">CertificateKeystores</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Additional keystore output formats to be stored in the Certificate&rsquo;s Secret.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuerRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ObjectReference">ObjectReference</a>
        </em>
      </td>
      <td>
        <p>Reference to the issuer responsible for issuing the certificate. If the issuer is namespace-scoped, it must be in the same namespace as the Certificate. If the issuer is cluster-scoped, it can be used from any namespace.</p>
        <p> The <code>name</code> field of the reference must always be specified. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>isCA</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Requested basic constraints isCA value. The isCA value is used to set the <code>isCA</code> field on the created CertificateRequest resources. Note that the issuer may choose to ignore the requested isCA value, just like any other requested attribute. </p>
        <p> If true, this will automatically add the <code>cert sign</code> usage to the list of requested <code>usages</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>usages</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.KeyUsage">[]KeyUsage</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Requested key usages and extended key usages. These usages are used to set the <code>usages</code> field on the created CertificateRequest resources. If <code>encodeUsagesInRequest</code> is unset or set to <code>true</code>, the usages will additionally be encoded in the <code>request</code> field which contains the CSR blob. </p>
        <p> If unset, defaults to <code>digital signature</code> and <code>key encipherment</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>privateKey</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Private key options. These include the key algorithm and size, the used encoding and the rotation policy.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>signatureAlgorithm</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.SignatureAlgorithm">SignatureAlgorithm</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Signature algorithm to use. Allowed values for RSA keys: SHA256WithRSA, SHA384WithRSA, SHA512WithRSA. Allowed values for ECDSA keys: ECDSAWithSHA256, ECDSAWithSHA384, ECDSAWithSHA512. Allowed values for Ed25519 keys: PureEd25519.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>encodeUsagesInRequest</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Whether the KeyUsage and ExtKeyUsage extensions should be set in the encoded CSR.</p>
        <p>This option defaults to true, and should only be disabled if the target issuer does not support CSRs with these X509 KeyUsage/ ExtKeyUsage extensions.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>revisionHistoryLimit</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          The maximum number of CertificateRequest revisions that are maintained in the Certificate&rsquo;s history. Each revision represents a single <code>CertificateRequest</code>
          created by this Certificate, either when it was created, renewed, or Spec was changed. Revisions will be removed by oldest first if the number of revisions exceeds this number.
        </p>
        <p> If set, revisionHistoryLimit must be a value of <code>1</code> or greater. Default value is <code>1</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>additionalOutputFormats</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateAdditionalOutputFormat">[]CertificateAdditionalOutputFormat</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Defines extra output formats of the private key and signed certificate chain to be written to this Certificate&rsquo;s target Secret.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>nameConstraints</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.NameConstraints">NameConstraints</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> x.509 certificate NameConstraint extension which MUST NOT be used in a non-CA certificate. More Info: <a href="https://datatracker.ietf.org/doc/html/rfc5280#section-4.2.1.10">https://datatracker.ietf.org/doc/html/rfc5280#section-4.2.1.10</a> </p>
        <p>
          This is an Alpha Feature and is only enabled with the
          <code>--feature-gates=NameConstraints=true</code> option set on both the controller and webhook components.
        </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.CertificateStatus">CertificateStatus</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.Certificate">Certificate</a>) </p>
<div>
  <p>CertificateStatus defines the observed state of Certificate</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>conditions</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CertificateCondition">[]CertificateCondition</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> List of status conditions to indicate the status of certificates. Known condition types are <code>Ready</code> and <code>Issuing</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastFailureTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastFailureTime is set only if the latest issuance for this Certificate failed and contains the time of the failure. If an issuance has failed, the delay till the next issuance will be calculated using formula time.Hour * 2 ^ (failedIssuanceAttempts - 1). If the latest issuance has succeeded this field will be unset.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>notBefore</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The time after which the certificate stored in the secret named by this resource in <code>spec.secretName</code> is valid. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>notAfter</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The expiration time of the certificate stored in the secret named by this resource in <code>spec.secretName</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>renewalTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>RenewalTime is the time at which the certificate will be next renewed. If not set, no upcoming renewal is scheduled.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>revision</code>
        <br />
        <em>int</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The current &lsquo;revision&rsquo; of the certificate as issued.</p>
        <p>
          When a CertificateRequest resource is created, it will have the
          <code>cert-manager.io/certificate-revision</code> set to one greater than the current value of this field.
        </p>
        <p>Upon issuance, this field will be set to the value of the annotation on the CertificateRequest resource used to issue the certificate.</p>
        <p>Persisting the value on the CertificateRequest resource allows the certificates controller to know whether a request is part of an old issuance or if it is part of the ongoing revision&rsquo;s issuance by checking if the revision value in the annotation is greater than this field.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>nextPrivateKeySecretName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>
          The name of the Secret resource containing the private key to be used for the next certificate iteration. The keymanager controller will automatically set this field if the
          <code>Issuing</code> condition is set to <code>True</code>. It will automatically unset this field when the Issuing condition is not set or False.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>failedIssuanceAttempts</code>
        <br />
        <em>int</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The number of continuous failed issuance attempts up till now. This field gets removed (if set) on a successful issuance and gets set to 1 if unset and an issuance has failed. If an issuance has failed, the delay till the next issuance will be calculated using formula time.Hour * 2 ^ (failedIssuanceAttempts - 1).</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.GenericIssuer">GenericIssuer</h3>
<div></div>
<h3 id="cert-manager.io/v1.IssuerCondition">IssuerCondition</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerStatus">IssuerStatus</a>) </p>
<div>
  <p>IssuerCondition contains condition information for an Issuer.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>type</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerConditionType">IssuerConditionType</a>
        </em>
      </td>
      <td>
        <p> Type of the condition, known values are (<code>Ready</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>status</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.ConditionStatus">ConditionStatus</a>
        </em>
      </td>
      <td>
        <p> Status of the condition, one of (<code>True</code>, <code>False</code>, <code>Unknown</code>). </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>lastTransitionTime</code>
        <br />
        <em>
          <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#time-v1-meta">Kubernetes meta/v1.Time</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>LastTransitionTime is the timestamp corresponding to the last status change of this condition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>reason</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reason is a brief machine readable explanation for the condition&rsquo;s last transition.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>message</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Message is a human readable description of the details of the last transition, complementing reason.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>observedGeneration</code>
        <br />
        <em>int64</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>If set, this represents the .metadata.generation that the condition was set based upon. For instance, if .metadata.generation is currently 12, but the .status.condition[x].observedGeneration is 9, the condition is out of date with respect to the current state of the Issuer.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.IssuerConditionType"> IssuerConditionType (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerCondition">IssuerCondition</a>) </p>
<div>
  <p>IssuerConditionType represents an Issuer condition value.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;Ready&#34;</p>
      </td>
      <td>
        <p> IssuerConditionReady represents the fact that a given Issuer condition is in ready state and able to issue certificates. If the <code>status</code> of this condition is <code>False</code>, CertificateRequest controllers should prevent attempts to sign certificates. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.IssuerConfig">IssuerConfig</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerSpec">IssuerSpec</a>) </p>
<div>
  <p>The configuration for the issuer. Only one of these can be set.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>acme</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuer">ACMEIssuer</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ACME configures this issuer to communicate with a RFC8555 (ACME) server to obtain signed x509 certificates.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ca</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.CAIssuer">CAIssuer</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>CA configures this issuer to sign certificates using a signing CA keypair stored in a Secret resource. This is used to build internal PKIs that are managed by cert-manager.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>vault</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VaultIssuer">VaultIssuer</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Vault configures this issuer to sign certificates using a HashiCorp Vault PKI backend.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>selfSigned</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.SelfSignedIssuer">SelfSignedIssuer</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>SelfSigned configures this issuer to &lsquo;self sign&rsquo; certificates using the private key used to create the CertificateRequest object.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>venafi</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VenafiIssuer">VenafiIssuer</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Venafi configures this issuer to sign certificates using a Venafi TPP or Venafi Cloud policy zone.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.IssuerSpec">IssuerSpec</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.ClusterIssuer">ClusterIssuer</a>, <a href="#cert-manager.io/v1.Issuer">Issuer</a>) </p>
<div>
  <p>IssuerSpec is the specification of an Issuer. This includes any configuration required for the issuer.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>IssuerConfig</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>
        </em>
      </td>
      <td>
        <p> (Members of <code>IssuerConfig</code> are embedded into this type.) </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.IssuerStatus">IssuerStatus</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.ClusterIssuer">ClusterIssuer</a>, <a href="#cert-manager.io/v1.Issuer">Issuer</a>) </p>
<div>
  <p>IssuerStatus contains status information about an Issuer</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>conditions</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.IssuerCondition">[]IssuerCondition</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> List of status conditions to indicate the status of a CertificateRequest. Known condition types are <code>Ready</code>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>acme</code>
        <br />
        <em>
          <a href="#acme.cert-manager.io/v1.ACMEIssuerStatus">ACMEIssuerStatus</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ACME specific status options. This field should only be set if the Issuer is configured to use an ACME server to issue certificates.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.JKSKeystore">JKSKeystore</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateKeystores">CertificateKeystores</a>) </p>
<div>
  <p>JKS configures options for storing a JKS keystore in the target secret. Either PasswordSecretRef or Password must be provided.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>create</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>
          Create enables JKS keystore creation for the Certificate. If true, a file named <code>keystore.jks</code> will be created in the target Secret resource, encrypted using the password stored in <code>passwordSecretRef</code> or <code>password</code>. The keystore file will be updated immediately. If the issuer provided a CA certificate, a file named <code>truststore.jks</code> will also be created in the target Secret resource, encrypted using the password stored in <code>passwordSecretRef</code>
          containing the issuing Certificate Authority
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>alias</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Alias specifies the alias of the key in the keystore, required by the JKS format. If not provided, the default alias <code>certificate</code> will be used. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>passwordSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>PasswordSecretRef is a reference to a non-empty key in a Secret resource containing the password used to encrypt the JKS keystore. Mutually exclusive with password. One of password or passwordSecretRef must provide a password with a non-zero length.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>password</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Password provides a literal password used to encrypt the JKS keystore. Mutually exclusive with passwordSecretRef. One of password or passwordSecretRef must provide a password with a non-zero length.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.KeyUsage"> KeyUsage (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateRequestSpec">CertificateRequestSpec</a>, <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>
    KeyUsage specifies valid usage contexts for keys. See:
    <a href="https://tools.ietf.org/html/rfc5280#section-4.2.1.3">https://tools.ietf.org/html/rfc5280#section-4.2.1.3</a>
    <a href="https://tools.ietf.org/html/rfc5280#section-4.2.1.12">https://tools.ietf.org/html/rfc5280#section-4.2.1.12</a>
  </p>
  <p>Valid KeyUsage values are as follows: &ldquo;signing&rdquo;, &ldquo;digital signature&rdquo;, &ldquo;content commitment&rdquo;, &ldquo;key encipherment&rdquo;, &ldquo;key agreement&rdquo;, &ldquo;data encipherment&rdquo;, &ldquo;cert sign&rdquo;, &ldquo;crl sign&rdquo;, &ldquo;encipher only&rdquo;, &ldquo;decipher only&rdquo;, &ldquo;any&rdquo;, &ldquo;server auth&rdquo;, &ldquo;client auth&rdquo;, &ldquo;code signing&rdquo;, &ldquo;email protection&rdquo;, &ldquo;s/mime&rdquo;, &ldquo;ipsec end system&rdquo;, &ldquo;ipsec tunnel&rdquo;, &ldquo;ipsec user&rdquo;, &ldquo;timestamping&rdquo;, &ldquo;ocsp signing&rdquo;, &ldquo;microsoft sgc&rdquo;, &ldquo;netscape sgc&rdquo;</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;any&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;crl sign&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;cert sign&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;client auth&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;code signing&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;content commitment&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;data encipherment&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;decipher only&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;digital signature&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;email protection&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;encipher only&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ipsec end system&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ipsec tunnel&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ipsec user&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;key agreement&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;key encipherment&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;microsoft sgc&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;netscape sgc&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ocsp signing&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;s/mime&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;server auth&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;signing&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;timestamping&#34;</p>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.NameConstraintItem">NameConstraintItem</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.NameConstraints">NameConstraints</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>dnsDomains</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>DNSDomains is a list of DNS domains that are permitted or excluded.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ipRanges</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>IPRanges is a list of IP Ranges that are permitted or excluded. This should be a valid CIDR notation.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>emailAddresses</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>EmailAddresses is a list of Email Addresses that are permitted or excluded.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>uriDomains</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>URIDomains is a list of URI domains that are permitted or excluded.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.NameConstraints">NameConstraints</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>NameConstraints is a type to represent x509 NameConstraints</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>critical</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>if true then the name constraints are marked critical.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>permitted</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.NameConstraintItem">NameConstraintItem</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Permitted contains the constraints in which the names must be located.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>excluded</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.NameConstraintItem">NameConstraintItem</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Excluded contains the constraints which must be disallowed. Any name matching a restriction in the excluded field is invalid regardless of information appearing in the permitted</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.OtherName">OtherName</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>oid</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>OID is the object identifier for the otherName SAN. The object identifier must be expressed as a dotted string, for example, &ldquo;1.2.840.113556.1.4.221&rdquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>utf8Value</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>utf8Value is the string value of the otherName SAN. The utf8Value accepts any valid UTF8 string to set as value for the otherName SAN.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.PKCS12Keystore">PKCS12Keystore</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateKeystores">CertificateKeystores</a>) </p>
<div>
  <p>
    PKCS12 configures options for storing a PKCS12 keystore in the
    <code>spec.secretName</code> Secret resource.
  </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>create</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p> Create enables PKCS12 keystore creation for the Certificate. If true, a file named <code>keystore.p12</code> will be created in the target Secret resource, encrypted using the password stored in <code>passwordSecretRef</code> or in <code>password</code>. The keystore file will be updated immediately. If the issuer provided a CA certificate, a file named <code>truststore.p12</code> will also be created in the target Secret resource, encrypted using the password stored in <code>passwordSecretRef</code> containing the issuing Certificate Authority </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>profile</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.PKCS12Profile">PKCS12Profile</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Profile specifies the key and certificate encryption algorithms and the HMAC algorithm used to create the PKCS12 keystore. Default value is <code>LegacyRC2</code> for backward compatibility. </p>
        <p>
          If provided, allowed values are:
          <code>LegacyRC2</code>: Deprecated. Not supported by default in OpenSSL 3 or Java 20. <code>LegacyDES</code>: Less secure algorithm. Use this option for maximal compatibility. <code>Modern2023</code>: Secure algorithm. Use this option in case you have to always use secure algorithms (e.g., because of company policy). Please note that the security of the algorithm is not that important in reality, because the unencrypted certificate and private key are also stored in the Secret.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>passwordSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>PasswordSecretRef is a reference to a non-empty key in a Secret resource containing the password used to encrypt the PKCS#12 keystore. Mutually exclusive with password. One of password or passwordSecretRef must provide a password with a non-zero length.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>password</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Password provides a literal password used to encrypt the PKCS#12 keystore. Mutually exclusive with passwordSecretRef. One of password or passwordSecretRef must provide a password with a non-zero length.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.PKCS12Profile"> PKCS12Profile (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.PKCS12Keystore">PKCS12Keystore</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;LegacyDES&#34;</p>
      </td>
      <td>
        <p> see: <a href="https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#LegacyDES">https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#LegacyDES</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;LegacyRC2&#34;</p>
      </td>
      <td>
        <p> see: <a href="https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#LegacyRC2">https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#LegacyRC2</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Modern2023&#34;</p>
      </td>
      <td>
        <p> see: <a href="https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#Modern2023">https://pkg.go.dev/software.sslmate.com/src/go-pkcs12#Modern2023</a> </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.PrivateKeyAlgorithm"> PrivateKeyAlgorithm (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;ECDSA&#34;</p>
      </td>
      <td>
        <p>ECDSA private key algorithm.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Ed25519&#34;</p>
      </td>
      <td>
        <p>Ed25519 private key algorithm.</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;RSA&#34;</p>
      </td>
      <td>
        <p>RSA private key algorithm.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.PrivateKeyEncoding"> PrivateKeyEncoding (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;PKCS1&#34;</p>
      </td>
      <td>
        <p> PKCS1 private key encoding. PKCS1 produces a PEM block that contains the private key algorithm in the header and the private key in the body. A key that uses this can be recognised by its <code>BEGIN RSA PRIVATE KEY</code> or <code>BEGIN EC PRIVATE KEY</code> header. NOTE: This encoding is not supported for Ed25519 keys. Attempting to use this encoding with an Ed25519 key will be ignored and default to PKCS8. </p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;PKCS8&#34;</p>
      </td>
      <td>
        <p> PKCS8 private key encoding. PKCS8 produces a PEM block with a static header and both the private key algorithm and the private key in the body. A key that uses this encoding can be recognised by its <code>BEGIN PRIVATE KEY</code> header. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.PrivateKeyRotationPolicy"> PrivateKeyRotationPolicy (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificatePrivateKey">CertificatePrivateKey</a>) </p>
<div>
  <p>Denotes how private keys should be generated or sourced when a Certificate is being issued.</p>
</div>
<h3 id="cert-manager.io/v1.SelfSignedIssuer">SelfSignedIssuer</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>) </p>
<div>
  <p>Configures an issuer to &lsquo;self sign&rsquo; certificates using the private key used to create the CertificateRequest object.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>crlDistributionPoints</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The CRL distribution points is an X.509 v3 certificate extension which identifies the location of the CRL from which the revocation of this certificate can be checked. If not set certificate will be issued without CDP. Values are strings.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.ServiceAccountRef">ServiceAccountRef</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VaultKubernetesAuth">VaultKubernetesAuth</a>) </p>
<div>
  <p> ServiceAccountRef is a service account used by cert-manager to request a token. Default audience is generated by cert-manager and takes the form <code>vault://namespace-name/issuer-name</code> for an Issuer and <code>vault://issuer-name</code> for a ClusterIssuer. The expiration of the token is also set by cert-manager to 10 minutes. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Name of the ServiceAccount used to request a token.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>audiences</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>TokenAudiences is an optional list of extra audiences to include in the token passed to Vault. The default token consisting of the issuer&rsquo;s namespace and name is always included.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.SignatureAlgorithm"> SignatureAlgorithm (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;ECDSAWithSHA256&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ECDSAWithSHA384&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;ECDSAWithSHA512&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;PureEd25519&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;SHA256WithRSA&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;SHA384WithRSA&#34;</p>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        <p>&#34;SHA512WithRSA&#34;</p>
      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VaultAppRole">VaultAppRole</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VaultAuth">VaultAuth</a>) </p>
<div>
  <p>VaultAppRole authenticates with Vault using the App Role auth mechanism, with the role and secret stored in a Kubernetes Secret resource.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>path</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Path where the App Role authentication backend is mounted in Vault, e.g: &ldquo;approle&rdquo;</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>roleId</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>RoleID configured in the App Role authentication backend when setting up the authentication backend in Vault.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <p> Reference to a key in a Secret that contains the App Role secret used to authenticate with Vault. The <code>key</code> field must be specified and denotes which entry within the Secret resource is used as the app role secret. </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VaultAuth">VaultAuth</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VaultIssuer">VaultIssuer</a>) </p>
<div>
  <p> VaultAuth is configuration used to authenticate with a Vault server. The order of precedence is [<code>tokenSecretRef</code>, <code>appRole</code>, <code>clientCertificate</code> or <code>kubernetes</code>]. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>tokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>TokenSecretRef authenticates with Vault by presenting a token.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>appRole</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VaultAppRole">VaultAppRole</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>AppRole authenticates with Vault using the App Role auth mechanism, with the role and secret stored in a Kubernetes Secret resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clientCertificate</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VaultClientCertificateAuth">VaultClientCertificateAuth</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ClientCertificate authenticates with Vault by presenting a client certificate during the request&rsquo;s TLS handshake. Works only when using HTTPS protocol.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>kubernetes</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VaultKubernetesAuth">VaultKubernetesAuth</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Kubernetes authenticates with Vault by passing the ServiceAccount token stored in the named Secret resource to the Vault server.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VaultClientCertificateAuth">VaultClientCertificateAuth</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VaultAuth">VaultAuth</a>) </p>
<div>
  <p>VaultKubernetesAuth is used to authenticate against Vault using a client certificate stored in a Secret.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>mountPath</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The Vault mountPath here is the mount path to use when authenticating with Vault. For example, setting a value to <code>/v1/auth/foo</code>, will use the path <code>/v1/auth/foo/login</code> to authenticate with Vault. If unspecified, the default value &ldquo;/v1/auth/cert&rdquo; will be used. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reference to Kubernetes Secret of type &ldquo;kubernetes.io/tls&rdquo; (hence containing tls.crt and tls.key) used to authenticate to Vault using TLS client authentication.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Name of the certificate role to authenticate against. If not set, matching any certificate role, if available.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VaultIssuer">VaultIssuer</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>) </p>
<div>
  <p>Configures an issuer to sign certificates using a HashiCorp Vault PKI backend.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>auth</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VaultAuth">VaultAuth</a>
        </em>
      </td>
      <td>
        <p>Auth configures how cert-manager authenticates with the Vault server.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>server</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> Server is the connection address for the Vault server, e.g: &ldquo;<a href='https://vault.example.com:8200"'>https://vault.example.com:8200&rdquo;</a>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>serverName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>ServerName is used to verify the hostname on the returned certificates by the Vault server.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>path</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> Path is the mount path of the Vault PKI backend&rsquo;s <code>sign</code> endpoint, e.g: &ldquo;my_pki_mount/sign/my-role-name&rdquo;. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>namespace</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> Name of the vault namespace. Namespaces is a set of features within Vault Enterprise that allows Vault environments to support Secure Multi-tenancy. e.g: &ldquo;ns1&rdquo; More about namespaces can be found here <a href="https://www.vaultproject.io/docs/enterprise/namespaces">https://www.vaultproject.io/docs/enterprise/namespaces</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>caBundle</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Base64-encoded bundle of PEM CAs which will be used to validate the certificate chain presented by Vault. Only used if using HTTPS to connect to Vault and ignored for HTTP connections. Mutually exclusive with CABundleSecretRef. If neither CABundle nor CABundleSecretRef are defined, the certificate bundle in the cert-manager controller container is used to validate the TLS connection.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>caBundleSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reference to a Secret containing a bundle of PEM-encoded CAs to use when verifying the certificate chain presented by Vault when using HTTPS. Mutually exclusive with CABundle. If neither CABundle nor CABundleSecretRef are defined, the certificate bundle in the cert-manager controller container is used to validate the TLS connection. If no key for the Secret is specified, cert-manager will default to &lsquo;ca.crt&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clientCertSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reference to a Secret containing a PEM-encoded Client Certificate to use when the Vault server requires mTLS.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clientKeySecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reference to a Secret containing a PEM-encoded Client Private Key to use when the Vault server requires mTLS.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VaultKubernetesAuth">VaultKubernetesAuth</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VaultAuth">VaultAuth</a>) </p>
<div>
  <p>Authenticate against Vault using a Kubernetes ServiceAccount token stored in a Secret.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>mountPath</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The Vault mountPath here is the mount path to use when authenticating with Vault. For example, setting a value to <code>/v1/auth/foo</code>, will use the path <code>/v1/auth/foo/login</code> to authenticate with Vault. If unspecified, the default value &ldquo;/v1/auth/kubernetes&rdquo; will be used. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>secretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>The required Secret field containing a Kubernetes ServiceAccount JWT used for authenticating with Vault. Use of &lsquo;ambient credentials&rsquo; is not supported.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>serviceAccountRef</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.ServiceAccountRef">ServiceAccountRef</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>A reference to a service account that will be used to request a bound token (also known as &ldquo;projected token&rdquo;). Compared to using &ldquo;secretRef&rdquo;, using this field means that you don&rsquo;t rely on statically bound tokens. To use this field, you must configure an RBAC rule to let cert-manager request a token.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>role</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>A required field containing the Vault Role to assume. A Role binds a Kubernetes ServiceAccount with a set of Vault policies.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VenafiCloud">VenafiCloud</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VenafiIssuer">VenafiIssuer</a>) </p>
<div>
  <p>VenafiCloud defines connection configuration details for Venafi Cloud</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> URL is the base URL for Venafi Cloud. Defaults to &ldquo;<a href='https://api.venafi.cloud/"'>https://api.venafi.cloud/&rdquo;</a>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiTokenSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <p>APITokenSecretRef is a secret key selector for the Venafi Cloud API token.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VenafiIssuer">VenafiIssuer</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.IssuerConfig">IssuerConfig</a>) </p>
<div>
  <p>Configures an issuer to sign certificates using a Venafi TPP or Cloud policy zone.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>zone</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Zone is the Venafi Policy Zone to use for this issuer. All requests made to the Venafi platform will be restricted by the named zone policy. This field is required.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tpp</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VenafiTPP">VenafiTPP</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>TPP specifies Trust Protection Platform configuration settings. Only one of TPP or Cloud may be specified.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>cloud</code>
        <br />
        <em>
          <a href="#cert-manager.io/v1.VenafiCloud">VenafiCloud</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Cloud specifies the Venafi cloud configuration settings. Only one of TPP or Cloud may be specified.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.VenafiTPP">VenafiTPP</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VenafiIssuer">VenafiIssuer</a>) </p>
<div>
  <p>VenafiTPP defines connection configuration details for a Venafi TPP instance</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>url</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> URL is the base URL for the vedsdk endpoint of the Venafi TPP instance, for example: &ldquo;<a href='https://tpp.example.com/vedsdk"'>https://tpp.example.com/vedsdk&rdquo;</a>. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>credentialsRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.LocalObjectReference">LocalObjectReference</a>
        </em>
      </td>
      <td>
        <p>CredentialsRef is a reference to a Secret containing the Venafi TPP API credentials. The secret must contain the key &lsquo;access-token&rsquo; for the Access Token Authentication, or two keys, &lsquo;username&rsquo; and &lsquo;password&rsquo; for the API Keys Authentication.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>caBundle</code>
        <br />
        <em>[]byte</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Base64-encoded bundle of PEM CAs which will be used to validate the certificate chain presented by the TPP server. Only used if using HTTPS; ignored for HTTP. If undefined, the certificate bundle in the cert-manager controller container is used to validate the chain.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>caBundleSecretRef</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>
        </em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Reference to a Secret containing a base64-encoded bundle of PEM CAs which will be used to validate the certificate chain presented by the TPP server. Only used if using HTTPS; ignored for HTTP. Mutually exclusive with CABundle. If neither CABundle nor CABundleSecretRef is defined, the certificate bundle in the cert-manager controller container is used to validate the TLS connection.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="cert-manager.io/v1.X509Subject">X509Subject</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>X509Subject Full X509 name specification</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>organizations</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Organizations to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>countries</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Countries to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>organizationalUnits</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Organizational Units to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>localities</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Cities to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>provinces</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>State/Provinces to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>streetAddresses</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Street addresses to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>postalCodes</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Postal codes to be used on the Certificate.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>serialNumber</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Serial number to be used on the Certificate.</p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<h2 id="controller.config.cert-manager.io/v1alpha1">controller.config.cert-manager.io/v1alpha1</h2>
<div>
  <p>Package v1alpha1 is the v1alpha1 version of the controller config API.</p>
</div>
<p>Resource Types:</p>
<ul></ul>
<h3 id="controller.config.cert-manager.io/v1alpha1.ACMEDNS01Config">ACMEDNS01Config</h3>
<p> (<em>Appears on:</em> <a href="#controller.config.cert-manager.io/v1alpha1.ControllerConfiguration">ControllerConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>recursiveNameservers</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p> Each nameserver can be either the IP address and port of a standard recursive DNS server, or the endpoint to an RFC 8484 DNS over HTTPS endpoint. For example, the following values are valid: - &ldquo;8.8.8.8:53&rdquo; (Standard DNS) - &ldquo;<a href='https://1.1.1.1/dns-query"'>https://1.1.1.1/dns-query&rdquo;</a> (DNS over HTTPS) </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>recursiveNameserversOnly</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>When true, cert-manager will only ever query the configured DNS resolvers to perform the ACME DNS01 self check. This is useful in DNS constrained environments, where access to authoritative nameservers is restricted. Enabling this option could cause the DNS01 self check to take longer due to caching performed by the recursive nameservers.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>checkRetryPeriod</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.Duration</em>
      </td>
      <td>
        <p>The duration the controller should wait between a propagation check. Despite the name, this flag is used to configure the wait period for both DNS01 and HTTP01 challenge propagation checks. For DNS01 challenges the propagation check verifies that a TXT record with the challenge token has been created. For HTTP01 challenges the propagation check verifies that the challenge token is served at the challenge URL. This should be a valid duration string, for example 180s or 1h</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="controller.config.cert-manager.io/v1alpha1.ACMEHTTP01Config">ACMEHTTP01Config</h3>
<p> (<em>Appears on:</em> <a href="#controller.config.cert-manager.io/v1alpha1.ControllerConfiguration">ControllerConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>solverImage</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The Docker image to use to solve ACME HTTP01 challenges. You most likely will not need to change this parameter unless you are testing a new feature or developing cert-manager.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverResourceRequestCPU</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Defines the resource request CPU size when spawning new ACME HTTP01 challenge solver pods.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverResourceRequestMemory</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Defines the resource request Memory size when spawning new ACME HTTP01 challenge solver pods.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverResourceLimitsCPU</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Defines the resource limits CPU size when spawning new ACME HTTP01 challenge solver pods.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverResourceLimitsMemory</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Defines the resource limits Memory size when spawning new ACME HTTP01 challenge solver pods.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverRunAsNonRoot</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Defines the ability to run the http01 solver as root for troubleshooting issues</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>solverNameservers</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p>A list of comma separated dns server endpoints used for ACME HTTP01 check requests. This should be a list containing host and port, for example [&ldquo;8.8.8.8:53&rdquo;,&ldquo;8.8.4.4:53&rdquo;] Allows specifying a list of custom nameservers to perform HTTP01 checks on.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="controller.config.cert-manager.io/v1alpha1.ControllerConfiguration">ControllerConfiguration</h3>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>kubeConfig</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>kubeConfig is the kubeconfig file used to connect to the Kubernetes apiserver. If not specified, the controller will attempt to load the in-cluster-config.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiServerHost</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> apiServerHost is used to override the API server connection address. Deprecated: use <code>kubeConfig</code> instead. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>kubernetesAPIQPS</code>
        <br />
        <em>float32</em>
      </td>
      <td>
        <p> Indicates the maximum queries-per-second requests to the Kubernetes apiserver TODO: floats are not recommended. Maybe we should use resource.Quantity? <a href="https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/quantity/">https://kubernetes.io/docs/reference/kubernetes-api/common-definitions/quantity/</a> </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>kubernetesAPIBurst</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <p>The maximum burst queries-per-second of requests sent to the Kubernetes apiserver</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>namespace</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>If set, this limits the scope of cert-manager to a single namespace and ClusterIssuers are disabled. If not specified, all namespaces will be watched</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clusterResourceNamespace</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Namespace to store resources owned by cluster scoped resources such as ClusterIssuer in.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>leaderElectionConfig</code>
        <br />
        <em>
          <a href="#controller.config.cert-manager.io/v1alpha1.LeaderElectionConfig">LeaderElectionConfig</a>
        </em>
      </td>
      <td>
        <p>LeaderElectionConfig configures the behaviour of the leader election</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>controllers</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p> A list of controllers to enable. [&rsquo;<em>&rsquo;] enables all controllers, [&lsquo;foo&rsquo;] enables only the foo controller [&rsquo;</em>&rsquo;, &lsquo;-foo&rsquo;] disables the controller named foo. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>issuerAmbientCredentials</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Whether an issuer may make use of ambient credentials. &lsquo;Ambient Credentials&rsquo; are credentials drawn from the environment, metadata services, or local files which are not explicitly configured in the Issuer API object. When this flag is enabled, the following sources for credentials are also used: AWS - All sources the Go SDK defaults to, notably including any EC2 IAM roles available via instance metadata.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>clusterIssuerAmbientCredentials</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Whether a cluster-issuer may make use of ambient credentials for issuers. &lsquo;Ambient Credentials&rsquo; are credentials drawn from the environment, metadata services, or local files which are not explicitly configured in the ClusterIssuer API object. When this flag is enabled, the following sources for credentials are also used: AWS - All sources the Go SDK defaults to, notably including any EC2 IAM roles available via instance metadata.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enableCertificateOwnerRef</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Whether to set the certificate resource as an owner of secret where the tls certificate is stored. When this flag is enabled, the secret will be automatically removed when the certificate resource is deleted.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enableGatewayAPI</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Whether gateway API integration is enabled within cert-manager. The ExperimentalGatewayAPISupport feature gate must also be enabled (default as of 1.15).</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>copiedAnnotationPrefixes</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p>Specify which annotations should/shouldn&rsquo;t be copied from Certificate to CertificateRequest and Order, as well as from CertificateSigningRequest to Order, by passing a list of annotation key prefixes. A prefix starting with a dash(-) specifies an annotation that shouldn&rsquo;t be copied. Example: &lsquo;*,-kubectl.kubernetes.io/&rsquo;- all annotations will be copied apart from the ones where the key is prefixed with &lsquo;kubectl.kubernetes.io/&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>numberOfConcurrentWorkers</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <p>The number of concurrent workers for each controller.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>maxConcurrentChallenges</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <p>The maximum number of challenges that can be scheduled as &lsquo;processing&rsquo; at once.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsListenAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port that the metrics endpoint should listen on.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsTLSConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.TLSConfig</em>
      </td>
      <td>
        <p>TLS config for the metrics endpoint</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>healthzListenAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port address, separated by a &lsquo;:&rsquo;, that the healthz server should listen on.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enablePprof</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>Enable profiling for controller.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>pprofAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port that Go profiler should listen on, i.e localhost:6060. Ensure that profiler is not exposed on a public address. Profiler will be served at /debug/pprof.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>logging</code>
        <br />
        <em>k8s.io/component-base/logs/api/v1.LoggingConfiguration</em>
      </td>
      <td>
        <p>
          logging configures the logging behaviour of the controller.
          <a href="https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration">https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration</a>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>featureGates</code>
        <br />
        <em>map[string]bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>featureGates is a map of feature names to bools that enable or disable experimental features.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>ingressShimConfig</code>
        <br />
        <em>
          <a href="#controller.config.cert-manager.io/v1alpha1.IngressShimConfig">IngressShimConfig</a>
        </em>
      </td>
      <td>
        <p>ingressShimConfig configures the behaviour of the ingress-shim controller</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>acmeHTTP01Config</code>
        <br />
        <em>
          <a href="#controller.config.cert-manager.io/v1alpha1.ACMEHTTP01Config">ACMEHTTP01Config</a>
        </em>
      </td>
      <td>
        <p>acmeHTTP01Config configures the behaviour of the ACME HTTP01 challenge solver</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>acmeDNS01Config</code>
        <br />
        <em>
          <a href="#controller.config.cert-manager.io/v1alpha1.ACMEDNS01Config">ACMEDNS01Config</a>
        </em>
      </td>
      <td>
        <p>acmeDNS01Config configures the behaviour of the ACME DNS01 challenge solver</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="controller.config.cert-manager.io/v1alpha1.IngressShimConfig">IngressShimConfig</h3>
<p> (<em>Appears on:</em> <a href="#controller.config.cert-manager.io/v1alpha1.ControllerConfiguration">ControllerConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>defaultIssuerName</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Default issuer/certificates details consumed by ingress-shim Name of the Issuer to use when the tls is requested but issuer name is not specified on the ingress resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>defaultIssuerKind</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Kind of the Issuer to use when the TLS is requested but issuer kind is not specified on the ingress resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>defaultIssuerGroup</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Group of the Issuer to use when the TLS is requested but issuer group is not specified on the ingress resource.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>defaultAutoCertificateAnnotations</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p>The annotation consumed by the ingress-shim controller to indicate an ingress is requesting a certificate</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>extraCertificateAnnotations</code>
        <br />
        <em>[]string</em>
      </td>
      <td>
        <p>ExtraCertificateAnnotations is a list of annotations which should be copied from and ingress-like object to a Certificate.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="controller.config.cert-manager.io/v1alpha1.LeaderElectionConfig">LeaderElectionConfig</h3>
<p> (<em>Appears on:</em> <a href="#controller.config.cert-manager.io/v1alpha1.ControllerConfiguration">ControllerConfiguration</a>) </p>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>LeaderElectionConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.LeaderElectionConfig</em>
      </td>
      <td>
        <p> (Members of <code>LeaderElectionConfig</code> are embedded into this type.) </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>healthzTimeout</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.Duration</em>
      </td>
      <td>
        <p>Leader election healthz checks within this timeout period after the lease expires will still return healthy.</p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<h2 id="meta.cert-manager.io/v1">meta.cert-manager.io/v1</h2>
<div>
  <p>Package v1 contains meta types for cert-manager APIs</p>
</div>
<p>Resource Types:</p>
<ul></ul>
<h3 id="meta.cert-manager.io/v1.ConditionStatus"> ConditionStatus (<code>string</code> alias) </h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.CertificateCondition">CertificateCondition</a>, <a href="#cert-manager.io/v1.CertificateRequestCondition">CertificateRequestCondition</a>, <a href="#cert-manager.io/v1.IssuerCondition">IssuerCondition</a>) </p>
<div>
  <p>ConditionStatus represents a condition&rsquo;s status.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>&#34;False&#34;</p>
      </td>
      <td>
        <p>ConditionFalse represents the fact that a given condition is false</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;True&#34;</p>
      </td>
      <td>
        <p>ConditionTrue represents the fact that a given condition is true</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>&#34;Unknown&#34;</p>
      </td>
      <td>
        <p>ConditionUnknown represents the fact that a given condition is unknown</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="meta.cert-manager.io/v1.LocalObjectReference">LocalObjectReference</h3>
<p> (<em>Appears on:</em> <a href="#cert-manager.io/v1.VenafiTPP">VenafiTPP</a>, <a href="#meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</a>) </p>
<div>
  <p>A reference to an object in the same namespace as the referent. If the referent is a cluster-scoped resource (e.g., a ClusterIssuer), the reference instead refers to the resource with the given name in the configured &lsquo;cluster resource namespace&rsquo;, which is set as a flag on the controller component (and defaults to the namespace that cert-manager runs in).</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> Name of the resource being referred to. More info: <a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names">https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names</a> </p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="meta.cert-manager.io/v1.ObjectReference">ObjectReference</h3>
<p> (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ChallengeSpec">ChallengeSpec</a>, <a href="#acme.cert-manager.io/v1.OrderSpec">OrderSpec</a>, <a href="#cert-manager.io/v1.CertificateRequestSpec">CertificateRequestSpec</a>, <a href="#cert-manager.io/v1.CertificateSpec">CertificateSpec</a>) </p>
<div>
  <p>ObjectReference is a reference to an object with a given name, kind and group.</p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>name</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>Name of the resource being referred to.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>kind</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Kind of the resource being referred to.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>group</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>Group of the resource being referred to.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3 id="meta.cert-manager.io/v1.SecretKeySelector">SecretKeySelector</h3>
<p>
  (<em>Appears on:</em> <a href="#acme.cert-manager.io/v1.ACMEExternalAccountBinding">ACMEExternalAccountBinding</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuer">ACMEIssuer</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAcmeDNS">ACMEIssuerDNS01ProviderAcmeDNS</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAkamai">ACMEIssuerDNS01ProviderAkamai</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderAzureDNS">ACMEIssuerDNS01ProviderAzureDNS</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudDNS">ACMEIssuerDNS01ProviderCloudDNS</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderCloudflare">ACMEIssuerDNS01ProviderCloudflare</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderDigitalOcean">ACMEIssuerDNS01ProviderDigitalOcean</a>, <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRFC2136">ACMEIssuerDNS01ProviderRFC2136</a>,
  <a href="#acme.cert-manager.io/v1.ACMEIssuerDNS01ProviderRoute53">ACMEIssuerDNS01ProviderRoute53</a>, <a href="#cert-manager.io/v1.JKSKeystore">JKSKeystore</a>, <a href="#cert-manager.io/v1.PKCS12Keystore">PKCS12Keystore</a>, <a href="#cert-manager.io/v1.VaultAppRole">VaultAppRole</a>, <a href="#cert-manager.io/v1.VaultAuth">VaultAuth</a>, <a href="#cert-manager.io/v1.VaultIssuer">VaultIssuer</a>, <a href="#cert-manager.io/v1.VaultKubernetesAuth">VaultKubernetesAuth</a>, <a href="#cert-manager.io/v1.VenafiCloud">VenafiCloud</a>, <a href="#cert-manager.io/v1.VenafiTPP">VenafiTPP</a>)
</p>
<div>
  <p> A reference to a specific &lsquo;key&rsquo; within a Secret resource. In some instances, <code>key</code> is a required field. </p>
</div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>LocalObjectReference</code>
        <br />
        <em>
          <a href="#meta.cert-manager.io/v1.LocalObjectReference">LocalObjectReference</a>
        </em>
      </td>
      <td>
        <p> (Members of <code>LocalObjectReference</code> are embedded into this type.) </p>
        <p>The name of the Secret resource being referred to.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>key</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p> The key of the entry in the Secret resource&rsquo;s <code>data</code> field to be used. Some instances of this field may be defaulted, in others it may be required. </p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<h2 id="webhook.config.cert-manager.io/v1alpha1">webhook.config.cert-manager.io/v1alpha1</h2>
<div>
  <p>Package v1alpha1 is the v1alpha1 version of the webhook config API.</p>
</div>
<p>Resource Types:</p>
<ul></ul>
<h3 id="webhook.config.cert-manager.io/v1alpha1.WebhookConfiguration">WebhookConfiguration</h3>
<div></div>
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>securePort</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <p>securePort is the port number to listen on for secure TLS connections from the kube-apiserver. If 0, a random available port will be chosen. Defaults to 6443.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>healthzPort</code>
        <br />
        <em>int32</em>
      </td>
      <td>
        <p>healthzPort is the port number to listen on (using plaintext HTTP) for healthz connections. If 0, a random available port will be chosen. Defaults to 6080.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>tlsConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.TLSConfig</em>
      </td>
      <td>
        <p>tlsConfig is used to configure the secure listener&rsquo;s TLS settings.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>kubeConfig</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>kubeConfig is the kubeconfig file used to connect to the Kubernetes apiserver. If not specified, the webhook will attempt to load the in-cluster-config.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>apiServerHost</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p> apiServerHost is used to override the API server connection address. Deprecated: use <code>kubeConfig</code> instead. </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>enablePprof</code>
        <br />
        <em>bool</em>
      </td>
      <td>
        <p>enablePprof configures whether pprof is enabled.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>pprofAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>pprofAddress configures the address on which /debug/pprof endpoint will be served if enabled. Defaults to &lsquo;localhost:6060&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>logging</code>
        <br />
        <em>k8s.io/component-base/logs/api/v1.LoggingConfiguration</em>
      </td>
      <td>
        <p>
          logging configures the logging behaviour of the webhook.
          <a href="https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration">https://pkg.go.dev/k8s.io/component-base@v0.27.3/logs/api/v1#LoggingConfiguration</a>
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code>featureGates</code>
        <br />
        <em>map[string]bool</em>
      </td>
      <td>
        <em>(Optional)</em>
        <p>featureGates is a map of feature names to bools that enable or disable experimental features.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsListenAddress</code>
        <br />
        <em>string</em>
      </td>
      <td>
        <p>The host and port that the metrics endpoint should listen on. The value &ldquo;0&rdquo; disables the metrics server. Defaults to &lsquo;0.0.0.0:9402&rsquo;.</p>
      </td>
    </tr>
    <tr>
      <td>
        <code>metricsTLSConfig</code>
        <br />
        <em>github.com/cert-manager/cert-manager/pkg/apis/config/shared/v1alpha1.TLSConfig</em>
      </td>
      <td>
        <p>metricsTLSConfig is used to configure the metrics server TLS settings.</p>
      </td>
    </tr>
  </tbody>
</table>
<hr />
<p>
  <em> Generated with <code>gen-crd-api-reference-docs</code> on git commit <code>3ab737e</code>. </em>
</p>
