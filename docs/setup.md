# Setup

Add the plugin to your frontend app:

```bash
cd packages/app && yarn add @k-phoen/backstage-plugin-grafana
```

Configure the plugin in `app-config.yaml`. The proxy endpoint described below will allow the frontend
to authenticate with Grafana without exposing your API key to users.
[Create an API key](https://grafana.com/docs/grafana/latest/http_api/auth/#create-api-token) if you don't already have one. `Viewer` access will be enough.

```yaml
# app-config.yaml
proxy:
  '/grafana/api':
    # May be an internal DNS
    target: https://grafana.host/
    headers:
      Authorization: Bearer ${GRAFANA_TOKEN}

grafana:
  # Publicly accessible domain
  domain: https://monitoring.company.com
```

Expose the plugin to Backstage:

```ts
// packages/app/src/plugins.tsx

// other plugins...

export { grafanaPlugin } from '@k-phoen/backstage-plugin-grafana';
```

That's it! You can now update your entities pages to [display alerts](alerts-on-component-page.md) or [dashboards](dashboards-on-component-page.md) related to them.