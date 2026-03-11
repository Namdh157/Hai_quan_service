# WSO2 MI Data Services

Data Services (.dbs) allow you to expose various data sources as a web service.

## Data Sources
- **RDBMS:** MySQL, PostgreSQL, Oracle, etc.
- **Spreadsheets:** CSV, Excel.
- **NoSQL:** MongoDB.
- **Custom Java Data Sources.**

## Key Components
- **Queries:** SQL or other query types mapped to operations.
- **Operations:** The external interface (SOAP or REST).
- **Resources:** Mapping queries to REST resources (GET, POST, etc.).

## Best Practices
- Use named queries.
- Optimize indexing on the underlying database.
- Use appropriate transport protocols (HTTP/HTTPS).
