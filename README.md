# Firecrawl MCP server

Discover a bounded set of site URLs, choose one relevant page, and request its Markdown content. Provider billing, access restrictions and page-level failures remain visible.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `FIRECRAWL_API_KEY`



Credential help: https://docs.firecrawl.dev/api-reference/v2-openapi.json

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call map_site '{"url":"https://docs.firecrawl.dev","limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/firecrawl-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| map_site | Read | Discover up to 100 site URLs with a provider-side 10-second timeout. |
| scrape_page | Read | Fetch a selected URL as Markdown with a 10-second provider timeout. Check success and returned data rather than assuming complete site extraction. |

## Concrete workflow

Discover a bounded set of site URLs, choose one relevant page, and request its Markdown content. Provider billing, access restrictions and page-level failures remain visible.

1. map_site
2. scrape_page

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=firecrawl&integration=firecrawl-mcp&utm_source=github&utm_campaign=github-firecrawl-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/firecrawl/).

## Provenance and maintenance

- https://docs.firecrawl.dev/api-reference/v2-openapi.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
