# Fully Managed Purpose-Built Database Options  

### **DocumentDB (with MongoDB compatibility)**  
* Fully managed **document database**.  
* Compatible with MongoDB workloads (so existing MongoDB apps/tools can work with minimal changes).  
* Best for **JSON-like document storage**.  

---

### **Keyspaces (for Apache Cassandra)**  
* Fully managed, **serverless Cassandra-compatible database**.  
* Built for **wide-column data models**.  
* Best for **massive scale, high write throughput, low-latency workloads** (like IoT, time-series).  

---

### **MemoryDB for Redis**  
* Redis-compatible, **in-memory database**.  
* Ultra-fast performance (microsecond latency).  
* Best for **real-time apps, caching, session stores, leaderboards**.  

---

### **Neptune**  
* Fully managed **graph database**.  
* Supports **property graph (Gremlin)** and **RDF (SPARQL)** query languages.  
* Best for **fraud detection, knowledge graphs, social networks, recommendation engines**.  

---

### **Timestream**  
* Serverless, fully managed **time-series database**.  
* Optimized for **storing and querying trillions of time-series events**.  
* Best for **IoT telemetry, monitoring, analytics, real-time metrics**.  

---

### **Quantum Ledger Database (QLDB)**  
* Immutable, cryptographically verifiable **ledger database**.  
* Maintains a **complete, verifiable history of all changes over time**.  
* Best for **audit trails, financial transactions, compliance records**.  

---

## 📊 Comparison Table

| Service         | Data Model         | Best Use Cases |
|-----------------|--------------------|----------------|
| DocumentDB      | Document (JSON)    | Content management, user profiles, catalogs |
| Keyspaces       | Wide-column        | IoT, time-series, high-scale writes |
| MemoryDB        | In-memory (Redis)  | Real-time apps, caching, gaming leaderboards |
| Neptune         | Graph              | Fraud detection, social networks, recommendations |
| Timestream      | Time-series        | IoT telemetry, monitoring, analytics |
| QLDB            | Ledger             | Audit trails, compliance, financial transactions |
