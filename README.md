# ISBE TRUST ANCHOR

## Introduction

The ISBE TRUST ANCHOR is a set of rules and guidelines that define the trust relationships between the different entities in the ISBE ecosystem. The framework is composed of the following trusted lists:

## Trusted Lists
* Trusted Services List

## How-To Guides

### How-To insert a new value in the Trusted Lists

1. Fork the repository. You will need a <a href="https://github.com/" target="_blank">Github account</a> to do so.

2. Select the environment you want to add the organization to (DEV, STG, PRD --if you are not an ISBE developer, choose PRD by default).

3. Select the YAML file corresponding to the list you want to modify and edit it (i. e. "trusted-services-list.yaml" to add a new trusted service.
  
4. Click on commit changes and select "Create a new branch for this commit and start a pull request".

5. Create a pull request.

6. If the pull request is approved, the data will be added to the directory.

### Which data is needed to set a new entry into the Trusted Services List?

The trusted services list contains all the verified and authorized services within the dome ecosystem. these services have met the required standards for secure and trusted interactions. To add a new entry to the trusted services list, specific information must be provided in a yaml file, adhering to the structure outlined below.

| **Field**                                       | **Description**                                                                                                                                                                                                                                                                          |
|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **clientId**                                    | Should be a `did:key` or a unique identifier for your client. Using a `did:key` allows the verifier to obtain your public keys for signature verification without needing a separate JWKS endpoint.                                                                                      |
| **url**                                         | The base URL of your service or application.                                                                                                                                                                                                                                             |
| **redirectUris**                                | Must include all the URLs where you expect to receive authentication responses. These should be HTTPS URLs to ensure secure communication.                                                                                                                                               |
| **scopes**                                      | Currently, only `openid_learcredential` is accepted. This scope allows your service to request the necessary credentials.                                                                                                                                                                |
| **clientAuthenticationMethods**                 | Must be set to `["client_secret_jwt"]`, as this is the only supported authentication method.                                                                                                                                                                                             |
| **authorizationGrantTypes**                     | Must be set to `["authorization_code"]`, as this is the only supported grant type.                                                                                                                                                                                                       |
| **postLogoutRedirectUris**                      | Include URLs where users should be redirected after they log out from your service.                                                                                                                                                                                                      |
| **requireAuthorizationConsent**                 | Set to `false` because explicit user consent is not required in this flow.                                                                                                                                                                                                               |
| **requireProofKey**                             | Set to `false` as PKCE is not utilized.                                                                                                                                                                                                                                                  |
| **jwkSetUrl**                                   | If you're using a `did:key` for your clientId, you do not need to provide a `jwkSetUrl` because the verifier can derive your JWKS directly from the `did:key`. However, if you're not using a unique identifier, you must provide the `jwkSetUrl` where your public keys can be fetched. |
| **tokenEndpointAuthenticationSigningAlgorithm** | Must be set to `ES256`, as this is the only supported algorithm.                                                                                                                                                                                                                         |

**Example YAML entry:**

```yaml
clients:
  - clientId: "did:key:zDnaeypyWjzn54GuUP7PmDXiiggCyiG7ksMF7Unm7kjtEKBez"
    url: "https://servicecatalog.isbe.es"
    redirectUris: ["https://servicecatalog.isbe.es/auth/vc/callback"]
    scopes: ["openid_learcredential"]
    clientAuthenticationMethods: ["client_secret_jwt"]
    authorizationGrantTypes: ["authorization_code"]
    postLogoutRedirectUris: ["https://servicecatalog.isbe.es/"]
    requireAuthorizationConsent: false
    requireProofKey: false
    jwkSetUrl: "https://verifier.isbe.es/oidc/did/did:key:zDnaeypyWjzn54GuUP7PmDXiiggCyiG7ksMF7Unm7kjtEKBez"
    tokenEndpointAuthenticationSigningAlgorithm: "ES256"
```

