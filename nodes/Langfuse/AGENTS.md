# AGENTS.md - Langfuse Node

## OVERVIEW

Core node implementation for fetching Langfuse prompts using a declarative routing-based API pattern.

## WHERE TO LOOK

- `Langfuse.node.ts`: Primary file containing the `INodeType` class, property definitions, and API routing logic.
- `Langfuse.json`: Metadata for the node, including categories and documentation links.
- `langfuse.svg`: Icon used for the node in the n8n canvas.

## CONVENTIONS

- **Declarative Routing**: Unlike traditional nodes using an `execute()` method, this node uses `routing.request` within the `description.properties` array. This is the modern n8n approach for REST-heavy nodes.
- **Resource/Operation Structure**:
  - **Resource**: Currently supports `prompt`.
  - **Operation**: Supports `get` for prompt retrieval.
  - New operations should follow this nested structure to maintain UI consistency.
- **Input Parameters**:
  - `promptName`: Required string, interpolated directly into the URL path.
  - `label`: Required string with a default of `production`, passed as a query parameter.
- **UI Logic**: Uses `displayOptions.show` to conditionally render fields based on the selected `resource` and `operation`.
- **No-Data Expressions**: `noDataExpression: true` is set on the Resource and Operation fields to prevent users from using expressions for structural node settings.

## ROUTING NOTES

- **Authentication**: Credentials (`langfuseApi`) are automatically handled by the routing engine, injecting the necessary auth headers.
- **Base Configuration**:
  - `requestDefaults.baseURL`: Dynamically set via `{{$credentials.host}}`.
- **Endpoint Details**:
  - **Path**: `/api/public/v2/prompts/{{$parameter["promptName"]}}`
  - **Query String**: Handled via the `routing` object in the `label` property definition:
    ```typescript
    routing: {
      request: {
        qs: {
          label: '={{$value}}',
        },
      },
    }
    ```
- **Error Handling**: Standard n8n routing errors. If the API returns a non-2xx response, n8n handles the failure automatically unless custom `output` logic is added.
