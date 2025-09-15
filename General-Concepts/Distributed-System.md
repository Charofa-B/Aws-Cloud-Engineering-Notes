# Distributed Systems

<br><br>

## Multi-Tier Architecture (N-Tier)
* Software `architecture pattern` where an application is `divided` into `layers (tiers)`, each with its own `specific responsibility`.
* `Instead` of putting everything (UI, logic, database) in one system (`monolithic`), we `separate` them for scalability, maintainability, and security.

<br><br>

## Containers
* `Portable runtime` units that package an `application` with `all configs`, `libraries`, and `dependencies` it `needs`.
* `Lightweight` because they `share` the `host OS kernel` (not a full OS per app like VMs).
* `Isolated` → each `container` `runs independently`, but they can all `share the same host OS`.
* Scalable → you can `run` many `containers` (services) on `one host` or `across` a `cluster`.
* `Portable` → `Write once, run anywhere` (Linux, Windows, cloud, on-prem) → great for `any` programming `language`.

### Use Cases
* Microservices
* Batch Processing (ETL Jobs) – Efficient for `long-running data` `transformation` tasks that scale `dynamically`.
* Machine Learning (ML) Workloads
* Hybrid & Multi-Cloud Deployments
* Cloud Migration

<br><br>

## [Kubernetes (a.k.a. K8s)](#kubernetes)
* Open-source container orchestration platform.
* Automates deployment, scaling, and management of containerized applications.

### Features
* **Orchestration** → Manages `where` and `how containers run`.
* **Scaling** → `Automatically` `scales` apps up/down based on demand.
* **Load Balancing** → `Distributes traffic` across `containers`.
*  **Self-Healing** → `Restarts failed containers`, `replaces`, `reschedules`.
* **Service Discovery & Networking** → `Containers` can `find` and `talk` to `each other`.
* **Config & Secrets Management** → `Manages` `environment` `variables`, API keys, passwords.

### How it Works
**Cluster** → A `set of machines` (physical or virtual) running Kubernetes.
**Nodes** → `Worker machines where containers run`.
**Pods** → The `smallest` `deployable unit`, usually `holding 1` or `more containers`.
**Deployment** → `Tells` Kubernetes `how many` `copies` of a `pod` `should` run.
**Service** → `Exposes pods` to the network or other pods.
**Control Plane (Master Node)** → `Makes decisions`: scheduling, scaling, healing.

### Use Cases
* `Running microservices` applications at scale.
* `CI/CD pipelines` (automated deployments).
* `Hybrid cloud` and `multi-cloud apps`.
* `Batch jobs` and `data processing`.
* `Hosting web apps`, `APIs`, `AI/ML workloads`.

<br><br>

## Why Using Kubernetes Instead of Docker Swarm
Docker (specifically Docker Swarm) can do orchestration but Kubernetes has become the de facto standard.

1. **Ecosystem & Popularity**
* Kubernetes → `Industry standard`, `huge community`, `supported` by all major clouds (AWS, Azure, GCP).
* Docker Swarm → `Lightweight`, `simpler`, but `less widely adopted`.

2. **Scalability**
* Kubernetes → `Handles massive clusters` (thousands of nodes & containers).
* Docker Swarm → Better for `small to medium deployments`, less robust at huge scale.

3. **Networking**
* Kubernetes → `Rich networking model` with CNI plugins (Calico, Flannel, etc.), supports advanced routing, multi-cluster.
* Docker Swarm → Simple overlay networking, `limited flexibility`.

5. **Cloud-Native Integration**
* Kubernetes → `Deeply integrated into` Major `cloud players`, plus `on-prem` (`OpenShift`, `Rancher`).
* Docker Swarm → `Fewer managed service` offerings, more DIY.

<br><br>

## [Message Broker](#message-broker)
* Intermediary software that facilitates the exchange of information (messages) between different systems, applications, or services

### Key Concepts
* **Producer (Sender)** – The application or service that creates and `sends messages`.
* **Consumer (Receiver)** – The application or service that `receives` and `processes messages`.
* **Queue or Topic** – Logical `channels` where `messages` are `temporarily` `stored` until consumed.
* **Queue** → Point-to-point;` one consumer receives a message`.
* **Topic** → Publish/subscribe; `multiple subscribers receive the same message`.
* **Decoupling** – `Producers` and `consumers` do `not communicate directly`. The `broker` handles `delivery`, `buffering`, and `retry`.
* **Asynchronous Communication** – The `producer` can `send` `messages` `without` `waiting` for `consumers` to `process` them.

### What A Message Broker Does:
* `Receives messages` from producers.
* `Stores` and `routes` `messages` according to the delivery rules.
* `Delivers messages` to one or more consumers.
* `Handles failures` and retries if a consumer is unavailable.
* `Supports message ordering`, `filtering`, and `transformation` (optional, depending on the broker).

<br><br>

## [Apache ActiveMQ](#apache-activemq)
Open-source message `broker` that `implements` the `Java Message Service (JMS)` `API` with reliable, asynchronous, and decoupled messaging.

## Key Features
* **Message Queues & Topics** – Supports both `point-to-point` (`queues`) and `publish/subscribe` (`topics`) messaging patterns.
* **Protocols Support**
    * [JMS](https://activemq.apache.org/components/artemis/documentation/1.0.0/using-jms.html)
    * [AMQP](https://activemq.apache.org/components/classic/documentation/amqp)
    * [MQTT](https://activemq.apache.org/components/classic/documentation/mqtt)
    * [STOMP](https://activemq.apache.org/components/classic/documentation/stomp)
    * [OpenWire](https://activemq.apache.org/components/classic/documentation/openwire), and more.
* **Persistence** – Messages can be `persisted` to `disk` to survive `broker` restarts.
* **High Availability** – Supports `clustering` and `master/slave configurations`.
* **Message Filtering & Transformation**
* **Cross-Language Clients**
* **Supports Horizontal Scaling**

## Why Use ActiveMQ?
* `Ensures reliable delivery` even if consumers are temporarily down.
* `Supports complex enterprise` messaging patterns with `transactions` and `routing`.

<br><br>

## [RabbitMQ](#rabbitmq)
Open-source message broker built on the Advanced Message Queuing Protocol (AMQP)

## Key Features
* **Message Queues & Routing** – `Supports point-to-point queues` and `pub/sub (fanout exchanges)` flexible `routing` with `exchanges`.
* **Protocols Support**
    * [AMQP 0-9-1](https://www.rabbitmq.com/tutorials/amqp-concepts)
    * [AMQP 1.0](https://www.rabbitmq.com/docs/amqp)
    * [MQTT](https://www.rabbitmq.com/docs/mqtt)
    * [STOMP](https://activemq.apache.org/components/classic/documentation/stomp)
    * HTTP / Web STOMP
    * XMPP
* **Persistence & Reliability**
* **High Availability & Clustering** – Can run in `clusters` with `mirrored queues` for `failover`.
* **Flexible Delivery Modes** – Supports `synchronous` and `asynchronous` `messaging`, `delayed delivery`, and `TTL (time-to-live)` for messages.
* **Cross-Language Support**
* **Management & Monitoring** – Provides a `web-based management UI` and `CLI` for `inspecting queues, exchanges, and message flows`.
* **Supports load distribution across multiple queues**

<br><br>

# RabbitMQ Vs ActiveMQ
| Feature       | RabbitMQ                                      | ActiveMQ                                |
| ------------- | --------------------------------------------- | --------------------------------------- |
| Protocol      | AMQP (primary), MQTT, STOMP                   | JMS, AMQP, MQTT, STOMP, OpenWire        |
| Routing       | Exchanges + Queues, flexible routing patterns | Queues & Topics, simpler routing        |
| Popularity    | Modern microservices, cloud-native apps       | Enterprise Java & legacy systems        |
| Ease of Setup | Lightweight, easy to start                    | Heavier, more enterprise-oriented       |
| Performance   | High throughput with small messages           | Good, optimized for JMS enterprise apps |

<br><br>

## [Apache Kafka](#apache-kafka)

* `Open-source`, `distributed` event `streaming` platform.
* Mainly used to `publish` (write), `subscribe` (read), store, and `process` streams of `events` in `real time`.
* `High-throughput`, low-latency `event bus` for `moving data` between systems or applications.

### Not Just Messaging
* Stores events for a configurable retention period (not just transient like SNS).
* Allows replay of past messages.
* Supports stream processing (via Kafka Streams or KSQL).
* Provide real-time streaming (low-latency event ingestion and processing).
* Enables `multiple consumer groups` to independently read at their own pace.
* `Durable storage` of event logs (unlike SNS which doesn’t persist).
* High-throughput, low-latency real-time event streaming.

### Core Components
* **Producer**
    * `Application/service` that `writes (publishes)` data (`events/messages`) `to` `Kafka`.
* **Consumer**
    * `Application/service` that `reads (subscribes)` data `from` `Kafka`.
* **Topic**
    * Logical `channel/stream` to which `producers send` data and from which `consumers read`.
    * Can have `multiple channels`
* **Consumer Group** 
    * A `set of consumers` that share the `work of reading` from a topic.
    * Within a group, each `partition` is `read` by exactly `one consumer` → ensures `parallelism` `without duplication`.
    * `Multiple consumer groups` can `independently` `read` the `same topic`.
* **Partitions**
    * A topic is `divided` into partitions for `scalability` and `parallelism`.
    * Each `partition` is `ordered`, `immutable`, and `append-only`.
* **Brokers**
    * `Kafka servers` that `store` `partitions` and serve data to `producers/consumers`.
    * A `cluster` is a `group` of `brokers`.
* **ZooKeeper / KRaft**
    * Used to `manage` `cluster` `metadata` and `broker coordination` (newer versions move toward KRaft mode without ZooKeeper).

### How It Works
1. User `clicked button` → `Producer`
    * The app (producer) `sends` the `event` (message) to `Kafka`.
    * It `specifies` the `topic (channel)` and `optionally` a `partition key`.

2. `Broker receives` → `stores in topic/partition`
    * Kafka `Broker` `writes the event` into the `correct topic`.
    * If the topic `has partitions`, the event goes into one `specific partition` (decided by Kafka’s partitioning logic).
    * If the topic has `only one partition`, then everything `lands there`.

3. `Consumers subscribed` to the topic → read events
    * One or more `consumers` `subscribe` to the `topic`.
    * Each `consumer group` `ensures` that partitions are `distributed among consumers` for `parallel` processing.
    * Consumers process the event (e.g., logging it, updating analytics, triggering workflows).

### Kafka Connect
* Makes it easy to integrate Kafka with external systems.
* Instead of writing custom producer/consumer apps, you use `connectors (plugins)` to move data in and out of Kafka.
* Middleware layer between Kafka and other systems.
* Example connectors
    * Source connectors: Pull data into Kafka (e.g., from MySQL, DynamoDB, or S3).
    * Sink connectors: Push data out of Kafka (e.g., to Elasticsearch, Redshift, or S3).