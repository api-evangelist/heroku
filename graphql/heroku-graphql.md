# Heroku GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Heroku Platform API. Heroku exposes its platform capabilities through a REST API at `https://api.heroku.com`, documented at [https://devcenter.heroku.com/articles/platform-api-reference](https://devcenter.heroku.com/articles/platform-api-reference). The GraphQL schema below models the same domain objects as graph types, enabling clients to query related resources in a single request.

## Source

- **Provider:** Heroku (Salesforce)
- **REST API Docs:** https://devcenter.heroku.com/articles/platform-api-reference
- **Base URL:** https://api.heroku.com
- **GitHub:** https://github.com/heroku
- **Schema file:** heroku-schema.graphql

## Design Notes

The schema follows Heroku's resource hierarchy:

- **Account** is the root identity resource. Accounts own apps, teams, and OAuth clients.
- **App** is the central deployable unit. Apps have dynos, config vars, builds, releases, domains, add-ons, collaborators, log drains, and webhooks.
- **Pipeline** groups apps across stages (review, staging, production) via **PipelineCoupling**.
- **Space** represents a Private Space — a network-isolated runtime environment within a **Team**.
- **Add-on** resources (AddonService, AddonPlan, Addon, AddonAttachment) model the marketplace provisioning lifecycle.
- **OAuth** types (OAuthClient, OAuthAuthorization, OAuthToken, OAuthGrant) cover the full authorization code and token flow.
- **Webhook** types (Webhook, WebhookDelivery, WebhookEvent) cover the Heroku event delivery system.

## Type Summary

| Type | Description |
|------|-------------|
| Account | Heroku user account |
| AccountFeature | Optional feature flag on an account |
| App | Deployable application unit |
| AppFeature | Feature flag scoped to an app |
| AppFormation | Aggregate of all process formations for an app |
| AppSetup | Automated app creation from an app.json |
| AppWebhook | Alias for Webhook scoped to an app |
| Addon | Provisioned add-on instance attached to an app |
| AddonAttachment | Link between an add-on and an app |
| AddonConfig | Configuration key/value for an add-on |
| AddonPlan | Pricing tier for an add-on service |
| AddonService | Third-party service available in the marketplace |
| Build | Source build artifact compilation |
| Buildpack | Buildpack used in a build |
| BuildpackInstallation | Ordered buildpack on an app |
| Collaborator | User granted access to an app |
| ConfigVar | Key/value environment variable on an app |
| CreditCard | Payment card on file |
| Domain | Custom domain bound to an app |
| Dyno | Running process instance on an app |
| DynoSize | Available dyno compute tier |
| Enterprise Account | Enterprise account container |
| Formation | Process type and scale definition for an app |
| IdentityProvider | SAML IdP for SSO |
| Invoice | Billing invoice for an account or team |
| Key | SSH public key on an account |
| Log | Log line from a log stream |
| LogDrain | Log forwarding destination for an app |
| Maintenance | Maintenance window configuration for an app |
| OAuthAuthorization | OAuth authorization grant record |
| OAuthClient | Registered OAuth application |
| OAuthGrant | Authorization code within an OAuth flow |
| OAuthToken | Access token obtained via OAuth |
| OutboundRuleset | Firewall outbound ruleset for a Private Space |
| PasswordReset | Password reset request |
| PaymentMethod | Billing payment method |
| Pipeline | Named grouping of apps across stages |
| PipelineCoupling | Link between a pipeline and an app/stage |
| PipelinePromotion | Promotion of a slug from one stage to the next |
| PipelinePromotionTarget | Target app for a pipeline promotion |
| PipelineTransfer | Transfer of pipeline ownership |
| Region | Heroku infrastructure region |
| Release | Deployed version of an app |
| ReviewApp | Temporary app created for a pull request |
| ReviewAppConfig | Configuration for review app behavior |
| SNI | SNI SSL certificate on an app |
| SSLEndpoint | Legacy SSL endpoint on an app |
| Slug | Compiled executable artifact |
| Space | Heroku Private Space |
| SpaceAppAccess | App-level access grant within a Space |
| SpaceNAT | NAT configuration for outbound IPs in a Space |
| SpaceTopology | Network topology of a Space |
| SpaceTransfer | Transfer of space ownership |
| Stack | Heroku runtime stack (e.g., heroku-24) |
| Team | Heroku Team (formerly Organization) |
| TeamApp | App owned by a team |
| TeamAppPermission | Permission level for a team member on an app |
| TeamFeature | Feature flag scoped to a team |
| TeamInvitation | Pending team membership invitation |
| TeamMember | Member of a Heroku Team |
| Webhook | Outbound HTTP notification subscription |
| WebhookDelivery | Individual delivery attempt for a webhook event |
| WebhookEvent | Event payload delivered via a webhook |

## Authentication

Heroku uses Bearer token authentication. Requests must include:

```
Authorization: Bearer <token>
Accept: application/vnd.heroku+json; version=3
```

Tokens are obtained via the Heroku Dashboard, the CLI (`heroku auth:token`), or through the OAuth flow using OAuthClient / OAuthAuthorization / OAuthToken resources.

## Usage Example

This schema supports queries like:

```graphql
query GetAppDetails {
  app(id: "my-app-name") {
    id
    name
    region {
      name
    }
    stack {
      name
    }
    formation {
      process
      quantity
      size
    }
    releases(limit: 5) {
      version
      description
      createdAt
    }
    addons {
      name
      plan {
        name
        price {
          cents
          unit
        }
      }
    }
    domains {
      hostname
      kind
    }
    config {
      key
      value
    }
  }
}
```
