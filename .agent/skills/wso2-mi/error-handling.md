# WSO2 MI Error Handling

Robust error management is critical for enterprise integration.

## Fault Sequences
Messages are redirected to a fault sequence when an error occurs.
- **Properties set during fault:**
    - `ERROR_CODE`: Numerical code of the error.
    - `ERROR_MESSAGE`: Human-readable error message.
    - `ERROR_DETAIL`: Detailed stack trace or info.
    - `ERROR_EXCEPTION`: The exception object.

## Error Codes
- **101503:** Connection failed.
- **101504:** Connection timeout.
- **504821:** Application-level error from backend.

## MakeFault Mediator
Generates a custom error message to be sent back to the client or further handled.

## Retry Patterns
- **Message Store & Processor:** Decouples message ingestion from processing, allowing for retries and guaranteed delivery.
- **Dead Letter Channel:** Storing failed messages for manual intervention or delayed reprocessing.
