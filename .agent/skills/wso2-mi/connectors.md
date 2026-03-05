# WSO2 MI Connectors

Connectors allow MI to interact with external APIs and services using specialized operations.

## Common Connectors
- **HTTP:** Enhanced HTTP operations beyond standard endpoints.
- **Kafka:** Publishing and consuming messages from Kafka topics.
- **File:** Reading, writing, and moving files.
- **Salesforce, Gmail, etc.:** Cloud service integrations.

## Usage
1. **Import:** Add the connector dependency to `pom.xml`.
2. **Configure:** Define the connector configuration (credentials, URLs).
3. **Invoke:** Use the connector-specific tags in sequences.
```xml
<kafkaTransport.publish>
    <topic>orders</topic>
    <message>{...}</message>
</kafkaTransport.publish>
```
