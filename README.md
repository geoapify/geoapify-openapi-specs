# Geoapify OpenAPI specifications

Machine-readable [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0) definitions for Geoapify APIs and MCP tools. Use them to discover endpoints, inspect request and response schemas, generate clients, or provide tools to an AI agent.

[![Open API Explorer](https://img.shields.io/badge/Open_API_Explorer-Open_in_GitHub_Pages-1f6bff?style=for-the-badge&logo=swagger&logoColor=white)](https://geoapify.github.io/geoapify-openapi-specs/)

The specifications in `api-specs/` are generated artifacts. Their schemas are authoritative; this README provides discovery and usage guidance.

## AI and agent quick start

Start with [`api-specs/index.json`](api-specs/index.json), the machine-readable catalog of every specification in this repository.

1. Match the task to an entry using its `id`, `category`, and `description`.
2. Load the file named by `openApiSpec`. Paths are relative to `api-specs/index.json`.
3. Load only the selected specification unless the task requires multiple APIs. This reduces context use and avoids exposing unrelated operations to the agent.
4. Treat the selected OpenAPI document as the source of truth for endpoints, parameters, authentication, and schemas. Use `documentationUrl` for guides and examples.
5. Never invent an endpoint or parameter that is absent from the selected specification.

Example discovery with `jq`:

```bash
# List available specifications
jq -r '.apis[] | [.id, .title, .openApiSpec] | @tsv' api-specs/index.json

# Find routing-related specifications
jq '.apis[] | select((.id + " " + .description) | test("route|routing"; "i"))' api-specs/index.json
```

### Choosing an MCP specification

Use [`api-specs/mcp/tools/index.json`](api-specs/mcp/tools/index.json) to choose an MCP tool. Its descriptions explain when to use each tool and when another tool is a better match.

- Use a focused file under `api-specs/mcp/tools/` when an AI workflow needs one or a small number of tools. These definitions have explicit, typed operations and use less schema context.
- Use [`api-specs/mcp/mcp-api-openapi-specs.json`](api-specs/mcp/mcp-api-openapi-specs.json) when implementing or inspecting the complete MCP JSON-RPC endpoint. It contains all tool schemas behind one `POST /mcp` operation.

The focused files and aggregate MCP file describe the same service for different consumers. Keep both.

## Specification catalog

The catalog currently covers these groups:

| Group | APIs |
| --- | --- |
| Geocoding | Address Autocomplete, Batch Geocoding, Forward Geocoding, Reverse Geocoding |
| Routing | Routing, Route Matrix, Route Planner, Map Matching, Isoline |
| Places and location data | Places, Place Details, Place Info, Boundaries, Postcode, IP Geolocation, Elevation |
| Maps and geometry | Map Tiles, Static Maps, Map Marker, Geometry, Geometry Operations |
| Request orchestration | Batch API |
| MCP | Complete protocol specification and focused tool specifications |

Do not maintain a second exhaustive file list in this README. `api-specs/index.json` is generated with the specifications and prevents discovery information from drifting out of date.

## Authentication

Create an API key in the [Geoapify Projects dashboard](https://myprojects.geoapify.com/). Public API specifications support the authentication methods declared in each document, commonly:

- Query parameter: `apiKey=YOUR_API_KEY`
- Request header: `x-api-key: YOUR_API_KEY`

The header is preferable for server-to-server clients because URLs may be stored in logs, browser history, and analytics systems. Browser integrations may use the query parameter where required. MCP specifications use the `x-api-key` header.

Never commit a real API key to source control or embed a secret server key in public client code.

## Browse the specifications

Install dependencies and start the local Swagger UI:

```bash
npm install
npm start
```

Then open [http://localhost:8080/docs/index.html](http://localhost:8080/docs/index.html). The bundled Swagger UI supports the OpenAPI 3.1 definitions in this repository.

To use [Swagger Editor](https://editor.swagger.io/), import a raw specification URL such as:

```text
https://raw.githubusercontent.com/geoapify/geoapify-openapi-specs/main/api-specs/forward-geocoding/forward-geocoding-api-openapi-specs.json
```

## Generate a client

Use a generator and target that support OpenAPI 3.1. For example, with [OpenAPI Generator](https://openapi-generator.tech/):

```bash
npx @openapitools/openapi-generator-cli generate \
  -i api-specs/forward-geocoding/forward-geocoding-api-openapi-specs.json \
  -g typescript-fetch \
  -o generated-client
```

Generated clients may still require project-specific configuration, authentication handling, and runtime validation.

## Validate the specifications

Run the repository's Spectral rules against all OpenAPI files:

```bash
npm run lint
```

## Contributing

The specifications and discovery catalogs are generated artifacts. For schema changes, update the source and regenerate them instead of patching generated JSON. For repository tooling or documentation changes, open an issue or pull request in this repository.

## License

This repository is licensed under the [MIT License](LICENSE).
