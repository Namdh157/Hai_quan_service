# WSO2 MI Endpoints

Endpoints define the destination of a message.

## Common Endpoint Types

### Address Endpoint
Direct URL with specific configuration (format, optimization, soap version).
```xml
<address uri="http://example.com/api"/>
```

### HTTP Endpoint
Supports RESTful characteristics and URI templates.
```xml
<http method="POST" uri-template="http://example.com/users/{uri.var.id}"/>
```

### Default Endpoint
The destination is determined by the `To` header of the message.

## Load Balance and Failover

### Load Balance
Distributes traffic across multiple endpoints.
```xml
<loadbalance algorithm="roundrobin">
    <endpoint>...</endpoint>
    <endpoint>...</endpoint>
</loadbalance>
```

### Failover
If the primary endpoint fails, the message is sent to the secondary one.

## Configuration Options
- **Timeout:** Connection and socket timeouts.
- **Suspend on Failure:** Automatically suspends the endpoint if it returns errors.
- **Retry:** Configuration for retrying requests on failure.
