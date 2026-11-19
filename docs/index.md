# System Architecture Documentation
Welcome to the automated documentation site.

## Service Flow

<div id="mermaid-container"></div>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: false });
  
  const graphDefinition = `
    sequenceDiagram
      autonumber
      Client->>API Gateway: Request /data
      API Gateway->>Service: Fetch Data
      Service->>API Gateway: Return Payload
      API Gateway->>Client: 200 OK
  `;
  
  const { svg } = await mermaid.render('mermaid-svg', graphDefinition);
  document.getElementById('mermaid-container').innerHTML = svg;
</script>
