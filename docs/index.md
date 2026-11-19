# System Architecture Documentation
Welcome to the automated documentation site.

## Service Flow

<div class="mermaid">
sequenceDiagram
    autonumber
    Client->>API Gateway: Request /data
    API Gateway->>Service: Fetch Data
    Service->>API Gateway: Return Payload
    API Gateway->>Client: 200 OK
</div>
