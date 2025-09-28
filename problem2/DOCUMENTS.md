# Identity-Aware Proxy (IAP) and Pomerium

## Introduction to Identity-Aware Proxy (IAP)

### What is IAP?

An Identity-Aware Proxy (IAP) is a security tool that acts as an intermediary between users and protected resources, such as applications, servers, or services. It enforces access controls based on the user's identity, rather than relying solely on network-level protections like firewalls or VPNs. IAPs are designed to provide a centralized layer of authentication and authorization, ensuring that only verified users can access specific resources. This approach aligns with zero-trust security models, where trust is never assumed and must be continuously verified.

Unlike traditional proxies that might focus on routing or caching, an IAP integrates deeply with identity management systems. It evaluates access requests in real-time, considering factors beyond just credentials, such as the user's role, device state, location, or even the time of the request.

### What Does IAP Do?

IAP primarily secures access to internal or cloud-based resources by:

- **Authenticating Users**: Verifying who the user is through integration with identity providers (IdPs) like OAuth, SAML, or OpenID Connect.
- **Authorizing Access**: Determining what the user is allowed to do based on predefined policies. This can include role-based access control (RBAC), attribute-based access control (ABAC), or context-aware rules.
- **Proxying Traffic**: Routing approved requests to the backend resources while blocking unauthorized ones. It can also enrich requests by adding identity headers or tokens for downstream applications to consume.
- **Logging and Auditing**: Recording access attempts for compliance and security monitoring.

By doing so, IAP helps organizations move away from perimeter-based security (e.g., VPNs) to a more granular, identity-centric model. This is particularly useful for remote work, multi-cloud environments, and bring-your-own-device (BYOD) scenarios, where traditional network boundaries are ineffective.

### How Does IAP Work?

At a high level, an IAP operates through the following steps:

1. **Request Interception**: A user attempts to access a protected resource via a URL or endpoint. The IAP sits in front of the resource and intercepts the request.
2. **Authentication Check**: If the user isn't authenticated, the IAP redirects them to an IdP for login. Upon successful authentication, the IAP receives user identity details (e.g., via a token).
3. **Authorization Evaluation**: The IAP applies policies to the request. Policies might check attributes like user groups, device compliance, IP address, or request context. Access is granted only if all conditions are met.
4. **Proxy and Forward**: For approved requests, the IAP forwards the traffic to the backend, often adding headers with identity information for the application to use.
5. **Continuous Verification**: Unlike session-based access, advanced IAPs re-evaluate policies on a per-request basis, ensuring ongoing compliance.

This process eliminates the need for client-side software and supports seamless integration with existing infrastructure. IAPs can handle HTTP/HTTPS traffic and, in some cases, other protocols like TCP.

### Benefits and Applications of IAP

IAPs enhance security by reducing attack surfaces and enabling fine-grained controls. They are applied in scenarios such as:

- Securing web applications and APIs in cloud environments.
- Protecting on-premises resources for remote teams.
- Enforcing zero-trust access for developers, administrators, or third-party vendors.
- Integrating with CI/CD pipelines or Kubernetes clusters for service-to-service authentication.

Overall, IAP promotes scalability, reduces administrative overhead, and improves user experience by avoiding VPN logins.

## Introduction to Pomerium

### What is Pomerium?

Pomerium is an open-source identity-aware proxy that implements IAP principles to secure access to internal applications, servers, services, and workloads. It is built on the BeyondCorp model—a zero-trust framework pioneered by Google—and emphasizes continuous verification of identity, device state, and request context. Pomerium acts as a modern alternative to VPNs or tunnels, providing clientless access without requiring network reconfiguration.

As an IAP, Pomerium centralizes access policies, making it suitable for hybrid, cloud, and on-premises environments. It supports securing not just human users but also services and even AI agents, extending zero-trust principles to diverse use cases.

### Key Features of Pomerium

Pomerium offers a robust set of features that distinguish it as a versatile IAP:

- **Clientless Access**: No need for VPN clients or agents; users access resources via standard web browsers.
- **Granular Policy Enforcement**: Authenticates and authorizes every request, using context like identity, time, device posture, and location.
- **Extensibility**: Integrates with multiple IdPs (e.g., Google, Okta, Azure AD) and supports protocols beyond HTTP, including TCP.
- **Self-Hosted Control**: Keeps data, traffic, and policies within your environment, with options for open-source or enterprise editions.
- **Audit-Ready Logging**: Tracks every access decision for compliance, showing who accessed what, when, and why.
- **Performance and Scalability**: Lightweight deployment with high throughput, suitable for large-scale teams.
- **Open-Source Transparency**: Community-driven, with active development on GitHub, allowing customization and contributions.

Additional capabilities include role-based access control (RBAC), integration with Kubernetes Ingress, and support for passing identity details (e.g., as JWTs or headers) to upstream applications.

### How Pomerium Works

Pomerium functions as a reverse proxy that enforces zero-trust access. Here's a breakdown of its operation:

1. **Request Handling**: When a user or service requests a protected resource, Pomerium intercepts the traffic at a configured endpoint (e.g., a domain like app.example.com).
2. **Authentication**: If unauthenticated, Pomerium redirects the requester to an integrated IdP for login. It supports standards like OAuth2, OIDC, and SAML.
3. **Authorization**: Pomerium evaluates policies defined in YAML or via its console. Policies can incorporate contextual signals (e.g., user group membership, device health, or geolocation) to approve or deny access on a per-request basis.
4. **Proxying**: Approved requests are forwarded to the backend service. Pomerium can terminate TLS, add identity headers, or sign JWTs for the application to verify downstream.
5. **Continuous Monitoring**: Access isn't granted indefinitely; each subsequent request is re-verified, adapting to changes in context (e.g., a device becoming non-compliant).

This per-request model ensures dynamic security, contrasting with static session-based systems. Pomerium is protocol-aware, meaning it understands and inspects the content of requests for deeper authorization decisions.
