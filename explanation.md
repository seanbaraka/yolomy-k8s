Here's a concise summary of the key implementation decisions and reasoning:

1. **Kubernetes Objects Selection**
   - Frontend: Deployment (3 replicas) - stateless, needs scalability and rolling updates
   - Backend: Deployment (3 replicas) - stateless, configurable via secrets
   - Database: StatefulSet (3 replicas) - provides stable network IDs and persistent storage

2. **Exposing Services**
   - Frontend: LoadBalancer - public internet access via GKE load balancer
   - Backend: ClusterIP - internal access only, enhanced security
   - Database: Headless Service - enables direct pod-to-pod communication for replication

3. **Storage Strategy**
   - Used GKE Persistent Disks with dynamic provisioning
   - Implemented through volumeClaimTemplates for MongoDB
   - Each database pod gets its own persistent volume
   - Retention policy set to "Retain" for data safety

4. **Operational Aspects**
   - Monitoring: Prometheus, Grafana, Loki
   - Security: Network Policies, RBAC, Secrets management
   - Debug capabilities: Pod logs, events monitoring
   - Resource limits and requests configured for all components

This implementation provides a production-ready Kubernetes setup that balances scalability, security, and maintainability while following cloud-native best practices.
