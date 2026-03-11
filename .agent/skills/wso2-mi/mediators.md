# WSO2 MI Mediators

Mediators are the building blocks of WSO2 MI integration flows.

## Core Mediators

### Property Mediator
Sets or removes properties for the message context.
- **Scopes:** `default`, `axis2`, `transport`, `registry`.
- **Usage:** `<property name="MyProp" value="Value" scope="default" type="STRING"/>`

### Log Mediator
Logs message details.
- **Levels:** `simple`, `full`, `custom`.
- **Usage:** `<log level="custom"><property name="Message" value="Executing flow..."/></log>`

### PayloadFactory Mediator
Transforms or creates a new message payload.
- **Media Type:** `json`, `xml`.
- **Arguments:** Use `$1`, `$2`, etc., to inject values.
- **Usage:**
```xml
<payloadFactory media-type="json">
    <format>{"status": "$1", "data": "$2"}</format>
    <args>
        <arg evaluator="xml" expression="$ctx:status"/>
        <arg evaluator="xml" expression="$ctx:responseData"/>
    </args>
</payloadFactory>
```

### Call vs Send
- **Call:** Blocking call (usually inside a sequence). Continues execution after response.
- **Send:** Non-blocking/Asynchronous. Sends message and ends the sequence (or continues to out-path).

### Enrich Mediator
Modifies the message payload by adding, replacing, or deleting parts of it without recreating the whole payload.

### Filter & Switch
Logic branching for message flows.
```xml
<filter source="$ctx:Type" regex="JSON">
    <then>...</then>
    <else>...</else>
</filter>
```

## Advanced Mediators

### Class Mediator
Calls a custom Java class. Must implement `org.apache.synapse.ManagedLifecycle`.
```xml
<class name="com.example.CustomMediator"/>
```

### Script Mediator
Executes scripts (JavaScript, Ruby). Use sparingly for complex logic not possible with XML.
```xml
<script language="js">mc.setProperty("newProp", "computedValue");</script>
```
