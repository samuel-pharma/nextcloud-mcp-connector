# Security Policy

## Supported versions

Only the latest release of `mcp_connector` in the
[Nextcloud App Store](https://apps.nextcloud.com/apps/mcp_connector) is
supported. Please update before reporting.

## Reporting a vulnerability

Please do not open a public issue for a security problem.

- Preferred: GitHub private vulnerability reporting, via "Report a
  vulnerability" under the Security tab of this repository
- Alternative: mail to admin@infranode.dev

You will get a first answer within 7 days. Please include the connector
version, your Nextcloud version, the MCP client you used, and steps to
reproduce.

## Scope

The connector lets AI assistants work with a Nextcloud over MCP, with exactly
the rights of the signed-in user. The promises worth attacking: every request
acts as the user who completed the OAuth login and never beyond those rights,
tokens stay on the server running the connector, disabled tools
(`NC_MCP_DISABLED_TOOLS`) stay disabled, and no content leaves the machines
you operate. A report that breaks one of these is the most valuable kind.
