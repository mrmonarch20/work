# System Architecture Workflow

```mermaid
graph TD
    A[Client Browser] -->|HTTP Request| B[localhost:8080]
    B --> C[Nginx Reverse Proxy Container]
    
    C -->|/service1/*| D[Service1 Container<br/>Go App :8001]
    C -->|/service2/*| E[Service2 Container<br/>Python Flask :8002]
    
    D -->|JSON Response| C
    E -->|JSON Response| C
    C -->|Proxied Response| A
    
    subgraph "Docker Network"
        C
        D
        E
    end
    
    style A fill:#e1f5fe
    style C fill:#fff3e0
    style D fill:#e8f5e8
    style E fill:#fce4ec
```

## Request Flow Examples

### Service1 Request Flow
```
Client → localhost:8080/service1/ping 
      → Nginx (port 80) 
      → service1:8001/ping 
      → {"status":"ok","service":"1"}
```

### Service2 Request Flow  
```
Client → localhost:8080/service2/hello 
      → Nginx (port 80) 
      → service2:8002/hello 
      → {"message":"Hello from Service 2"}
```

## Container Communication
- **Network**: Docker bridge network
- **Service Discovery**: Container names (service1, service2, nginx)
- **Port Mapping**: Only nginx exposed to host (8080:80)
