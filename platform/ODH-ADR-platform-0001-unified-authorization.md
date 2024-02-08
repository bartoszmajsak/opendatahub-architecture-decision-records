# Open Data Hub - Unified OAuth2 Proxy Integration

<!-- copy and paste this template to start authoring your own ADR -->
<!-- remove this comment block too -->

|                |            |
| -------------- | ---------- |
| Date           | 02/08/2024 |
| Scope          | Platform + supported components |
| Status         | Draft |
| Authors        | [name](@github-username) |
| Supersedes     | N/A |
| Superseded by: | N/A |
| Tickets        | |
| Other docs:    | none |


## What

This ADR proposes the standardization of the OAuth2-Proxy integration across all components being part of Open Data Hub, transitioning from a disparate implementation strategy to a unified, platform-managed approach.

## Why

<!--- TODO

- [ ] add links to concrete implementations (or footnotes)

--->
The current implementation of using OAuth2-Proxy as a sidecar container by multiple component teams has resulted in incoherent strategies. These include mutating webhooks, Kustomize manifest overlays, templates processed by respective controllers and plain deployment YAML files. This diversity complicates platform governance, security auditing, and the onboarding process for new services.

## Goals

- Standardize the OAuth2 Proxy integration across all services.
- Simplify the authorization mechanism implementation for component teams.
- Enhance security and manageability through a centralized control mechanism.
- Operational Efficiency and Sustainability
  - Reduce overhead for component teams by providing a platform-managed service.
  - Minimize code maintenance costs by consolidating authorization configurations and reducing duplication.

## Non-Goals

- Replacing OAuth2 Proxy with a different authentication mechanism.

## How

Implement a platform-level component that manages OAuth2 Proxy configurations and injections based on service requirements. This component will provide inversion of control, allowing the platform team to ensure unified authorization approach while abstracting the complexity from service teams. Integration with the platform component will be achieved through annotations in service deployment manifests, enabling dynamic injection of the OAuth2 Proxy based on standardized policies.

## Open Questions

- What specific requirements do different component teams have for OAuth2 Proxy, and how can the platform component accommodate these?
- How will changes to the centralized OAuth2 Proxy configuration be rolled out to ensure minimal disruption to existing services?

## Alternatives

- **Continuing with the current approach:** Allows teams flexibility but does not address the issue of incoherence and the increased overhead for security and governance.
- **Mandatory use of Kustomize or mutating webhooks:** While more coherent than the current state, it still places the burden of implementation on component teams and lacks centralized control.

## Security and Privacy Considerations

The centralization of the OAuth2 Proxy integration enhances security by providing a consistent, auditable approach to authorization across the platform. However, it introduces a single point of failure and potential performance bottlenecks that need to be addressed in the component design.

## Risks

- Resistance from component teams due to perceived loss of control.
- Potential for increased latency or failure points in the service request path.
- Complexity in managing a centralized component that meets all service-specific requirements.

## Stakeholder Impacts

| Group                         | Key Contacts     | Date       | Impacted? |
| ----------------------------- | ---------------- | ---------- | --------- |
| group or team name            | key contact name | date       | ? |


## References

* optional bulleted list

## Reviews

| Reviewed by                   | Date       | Notes |
| ----------------------------- | ---------  | ------|
| name                          | date       | ? |
