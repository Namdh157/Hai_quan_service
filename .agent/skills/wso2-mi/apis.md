# WSO2 MI Synapse APIs

Synapse APIs provide a RESTful interface for integration services.

## API Structure
```xml
<api xmlns="http://ws.apache.org/ns/synapse" name="MyAPI" context="/myapi" version="1.0.0" version-type="url">
    <resource methods="GET" uri-template="/user/{id}">
        <inSequence>...</inSequence>
    </resource>
</api>
```

## Routing Logic
- **Context:** The base path for the API.
- **URI Template:** Defines path variables (e.g., `/user/{id}`).
- **URL Mapping:** Simple string matching for the sub-path.
- **Methods:** List of allowed HTTP verbs (GET, POST, PUT, DELETE, etc.).

## Resource Transformation
Use `PayloadFactory` within `inSequence` to normalize incoming requests.

## Shared Resources
API resources can use shared sequences via the `sequence` mediator.

## Standard Resource Template (Use Case Pattern)
When generating or modifying API paths (e.g., from Use Case documentation), ALWAYS follow this generalized structure:

1. **Header Comment**: Prefix each resource with `<!-- ================= UC[Number] ================= -->` (e.g., `<!-- ================= UC83 ================= -->`).
2. **Properties Extraction**: Extract all required variables at the start of `<inSequence>` (URI vars, XPath from payload, Headers).
   - Use `expression="get-property('uri.var.XXX')"` for path variables.
   - Use `expression="//XXX/text()"` for xml/json payload values.
   - Generate `backendPath` dynamically using `fn:concat()` if needed.
3. **Mandatory Field Validation (Filter)**: Check mandatory fields using `<filter xpath="string-length(get-property('XXX')) = 0">`.
   - If a required field is empty, return a 400 error via `<payloadFactory>` to formulate the error response, followed by `<respond/>`.
4. **Execution Logging**: If validation passes (`<else>` branch), log the execution using `<log level="custom">`.
   - Log the target `UseCase` (e.g., `UC83-ActionName`).
   - Log all extracted properties and the constructed `backendPath`.
5. **Backend Invocation**: Set the `Authorization` header inside the `transport` scope and invoke the backend service via `<http.post configKey="...">` (or appropriate method) using `<relativePath>{$ctx:backendPath}</relativePath>`.
6. **Respond**: Conclude the flow cleanly with `<respond/>`.

### Generic Code Structure Example:
```xml
    <!-- ================= UC[Number] ================= -->
    <resource methods="POST" uri-template="/{resourceId}/action">
        <inSequence>
            <!-- 1. Extract Properties -->
            <property name="resourceId" expression="get-property('uri.var.resourceId')" scope="default"/>
            <property name="requiredField" expression="//requiredField/text()" scope="default"/>
            <property name="authToken" expression="get-property('BackendAuthToken')" scope="default"/>
            <property name="backendPath" expression="fn:concat('/api/v1/resources/', get-property('resourceId'), '/action')" scope="default"/>

            <!-- 2. Validate Compulsory Fields -->
            <filter xpath="string-length(get-property('requiredField')) = 0">
                <then>
                    <property name="HTTP_SC" value="400" scope="axis2"/>
                    <payloadFactory media-type="xml">
                        <format>
                            <error>
                                <code>400</code><message>requiredField is required</message>
                            </error>
                        </format>
                        <args/>
                    </payloadFactory>
                    <respond/>
                </then>
                <else>
                    <!-- 3. Validation Passed -> Log Details -->
                    <log level="custom">
                        <property name="UseCase" value="UC[Number]-ActionName"/>
                        <property name="resourceId" expression="get-property('resourceId')"/>
                        <property name="requiredField" expression="get-property('requiredField')"/>
                        <property name="backendPath" expression="get-property('backendPath')"/>
                    </log>

                    <!-- 4. Backend Call -->
                    <header name="Authorization" expression="get-property('authToken')" scope="transport"/>
                    <http.post configKey="BackendConnection">
                        <relativePath>{$ctx:backendPath}</relativePath>
                    </http.post>
                    <respond/>
                </else>
            </filter>
        </inSequence>
    </resource>
```
