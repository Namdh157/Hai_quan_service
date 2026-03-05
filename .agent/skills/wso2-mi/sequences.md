# WSO2 MI Sequences

Sequences are ordered lists of mediators.

## Design Patterns

### Named Sequences
Reusable sequences defined in `src/main/wso2mi/artifacts/sequences`.
- Called using: `<sequence key="MySequence"/>`

### Inline Sequences
Sequences defined directly within an API resource or Proxy service.

### Main Sequence
The default flow for messages that don't match any other service.

### Fault Sequence
Handles errors during mediation. 
- **Local Fault:** Specific to a proxy/API.
- **Global Fault:** Default error handler for the server.

## Reusability Concepts
- **Local Entries:** Used to store static content or reusable configurations.
- **Templates:** Parameterized sequences for complex reuse across different flows.

## Best Practices
- Keep sequences focused (Single Responsibility Principle).
- Use descriptive names (e.g., `LogRequestSeq`, `TransformToInternalFormatSeq`).
- Always include logging for troubleshooting.
