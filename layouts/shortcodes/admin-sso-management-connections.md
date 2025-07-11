{{ $product_link := "[Docker Hub](https://hub.docker.com)" }}
{{ $sso_navigation := `Navigate to the SSO settings page for your organization. Select **My Hub**, your organization, **Settings**, and then **Security**.` }}

{{ if eq (.Get "product") "admin" }}
  {{ $product_link = "[Docker Home](https://app.docker.com) and select your organization. Note that when an organization is part of a company, you must select the company and configure SSO for that organization at the company level. Each organization can have its own SSO configuration and domain, but it must be configured at the company level." }}
  {{ $sso_navigation = "Select **Admin Console**, then **SSO and SCIM**." }}
{{ end }}

### Edit a connection

1. Sign in to {{ $product_link }}.
2. {{ $sso_navigation }}
3. In the SSO connections table, select the **Action** icon.
4. Select **Edit connection**.
5. Follow the on-screen instructions to edit the connection.

### Delete a connection

1. Sign in to {{ $product_link }}.
2. {{ $sso_navigation }}
3. In the SSO connections table, select the **Action** icon.
4. Select **Delete connection**.
5. Follow the on-screen instructions to delete a connection.

### Deleting SSO

When you disable SSO, you can delete the connection to remove the configuration settings and the added domains. Once you delete this connection, it can't be undone. If an SSO connection is deleted, Docker users must authenticate with their Docker ID and password.