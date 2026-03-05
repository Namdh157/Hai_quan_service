# WSO2 MI Synapse APIs

Synapse APIs provide a RESTful interface for integration services.

## API Structure
```xml
<api xmlns="http://ws.apache.org/ns/synapse" name="MyAPI" context="/myapi" version="1.0.0" version-type="url">
    <resource methods="GET" uri-template="/user/{id}">
        <inSequence>...</inSequence>
        <outSequence>...</outSequence>
        <faultSequence>...</faultSequence>
    </resource>
</api>
```

## Routing Logic
- **Context:** The base path for the API.
- **URI Template:** Defines path variables (e.g., `/user/{id}`).
- **URL Mapping:** Simple string matching for the sub-path.
- **Methods:** List of allowed HTTP verbs (GET, POST, PUT, DELETE, etc.).

## Resource Transformation
Use `PayloadFactory` within `inSequence` to normalize incoming requests and `outSequence` to format responses for the client.

## Shared Resources
API resources can use shared sequences via the `sequence` mediator.
