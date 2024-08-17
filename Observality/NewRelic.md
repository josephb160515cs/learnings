# New Relic

## Introduction
Observability in microservices architecture is essential due to the following reasons:

1. **Complexity Management**: Microservices involve numerous interconnected services, making it difficult to trace and diagnose issues. Observability provides visibility into how services interact.

2. **Real-time Monitoring**: It enables continuous monitoring of service health and performance, allowing for immediate detection and response to anomalies.

3. **Improved Debugging**: Detailed logs, metrics, and traces help in identifying the root cause of failures or performance bottlenecks across distributed services.

4. **Enhanced Reliability**: By proactively detecting issues, observability ensures services remain reliable, reducing downtime and maintaining user trust.

5. **Scalability**: As microservices scale, observability tools allow tracking of system behavior under load, ensuring consistent performance.

6. **Faster Incident Response**: With observability, teams can quickly identify and resolve issues, reducing Mean Time to Resolution (MTTR).

7. **Data-driven Decision Making**: Observability provides actionable insights that help in optimizing services and improving system architecture.

### Monitoring helps us answer 3 questions
* Is the service on?
* Is the service functioning as expected?
* Is the service performing well?

### Important metrics to measure observability suc
* MTTD - Mean time to detect - the time between the start of an issue and the time team becomes aware of it
* MTTR - Mean time to resolution - the time between the start of an issue and the time team takes to fix it or system becomes normal

### Methods of Observability
Typical m8s have 3 layers
* UI layer -observed via Core web vitals such as Percieved page load, Percieved page responsiveness, Percieved Stability)
* Service layer - observed by RED(Rate TPS, Error, Duration or latency) method
* Infrastructure layer - observed by USE (utilization, Saturation , Errors) method

### Types of Telemetry data
Telemetry data in observability is broadly categorized into 4 main types:

#### 1. **Logs**
- **Definition**: Logs are time-stamped, discrete records of events that occur within a system.
- **Usage**: Logs capture detailed information about specific events, such as errors, state changes, or user actions. They are crucial for debugging and understanding the sequence of operations.
- **Example**: An error log entry when a service fails to connect to a database.

#### 2. **Metrics**
- **Definition**: Metrics are numerical measurements that represent the state or performance of a system over time.
- **Usage**: Metrics are used for real-time monitoring, tracking trends, and alerting. They provide insights into resource utilization, latency, error rates, and other performance indicators.
- **Example**: CPU utilization percentage, request count per second, or memory usage.

#### 3. **Traces**
- **Definition**: Traces represent the journey of a request or transaction as it propagates through different services in a distributed system.
- **Usage**: Traces help in understanding the flow of requests across services, identifying bottlenecks, and diagnosing performance issues in microservices architectures.
- **Example**: A trace showing the path of an API call through multiple microservices, with details of time spent in each service.

#### 4. **Events**
- **Definition**: Events are significant state changes or conditions within a system.
- **Usage**: Events track specific occurrences that may require attention or action, such as scaling operations, deployment changes, or threshold breaches.
- **Example**: An event notification for a new service deployment or a scale-up operation.

> NOTE: Remember MELT as acronym

### Observality Platform
An observability platform is a comprehensive tool or suite of tools designed to provide visibility into the performance, health, and behavior of systems, particularly in complex environments like microservices architectures. It collects, processes, and analyzes telemetry data (logs, metrics, traces, etc.) to enable monitoring, troubleshooting, and optimization of services.

### Methods of Collecting Telemetry Data

1. **Agent-based Collection**
    - **Description**: Agents are lightweight software components installed on each service or host to collect telemetry data. They gather logs, metrics, and traces locally and forward them to the observability platform.
    - **Pros**:
        - **High Granularity**: Agents provide detailed, fine-grained data collection specific to each service or host.
        - **Customization**: Agents can be configured to collect specific types of data, offering flexibility.
        - **Low Latency**: Since agents run locally, data collection and transmission are typically fast.
    - **Cons**:
        - **Resource Overhead**: Agents consume system resources (CPU, memory), potentially impacting the performance of the host services.
        - **Management Complexity**: Maintaining and updating agents across multiple services can be challenging.
        - **Compatibility Issues**: Agents may need to be tailored to specific environments, leading to compatibility challenges.

2. **Sidecar Pattern**
    - **Description**: In microservices architectures, sidecar containers are deployed alongside the main service container. These sidecars handle tasks like telemetry data collection, networking, and monitoring without interfering with the primary service logic.
    - **Pros**:
        - **Isolation**: The sidecar pattern separates observability concerns from the main application, reducing complexity in the service code.
        - **Scalability**: As new services are deployed, sidecars can be easily added, ensuring consistent observability across the system.
        - **Portability**: Sidecars are containerized and can be deployed across different environments (e.g., Kubernetes).
    - **Cons**:
        - **Increased Resource Consumption**: Running additional sidecar containers increases the overall resource usage.
        - **Operational Complexity**: Managing sidecars for every service can add operational overhead, especially in large-scale deployments.
        - **Latency**: Introducing sidecars may slightly increase network latency due to the extra hop between the service and sidecar.

3. **Library Instrumentation**
    - **Description**: Libraries or SDKs are integrated directly into the application code to collect telemetry data. Developers instrument their code with these libraries to generate logs, metrics, and traces.
    - **Pros**:
        - **High Customization**: Developers have full control over what data is collected, allowing for tailored observability specific to business logic.
        - **Minimal Overhead**: Since the collection is embedded in the code, there’s no need for additional agents or sidecars.
        - **Direct Access**: Libraries can access internal application states directly, enabling precise data collection.
    - **Cons**:
        - **Developer Burden**: Instrumentation requires developers to modify code, adding to development effort and complexity.
        - **Code Coupling**: The application becomes tightly coupled with specific observability libraries, which can make future changes or migrations challenging.
        - **Performance Impact**: Poorly designed instrumentation can introduce performance overhead and slow down the application.

4. **Service Mesh**
    - **Description**: A service mesh is a dedicated infrastructure layer that handles communication between microservices. It can also capture telemetry data related to service-to-service communication, such as latency, errors, and traffic.
    - **Pros**:
        - **Transparent Operation**: The service mesh operates at the network level, requiring no changes to application code or deployment processes.
        - **Centralized Control**: It provides a consistent, centralized way to manage observability, security, and traffic policies across all services.
        - **Advanced Features**: Service meshes often come with built-in observability features, such as distributed tracing and traffic monitoring.
    - **Cons**:
        - **Complexity**: Deploying and managing a service mesh introduces additional complexity to the system architecture.
        - **Resource Overhead**: Running a service mesh consumes additional resources, particularly in terms of CPU and memory.
        - **Latency**: The service mesh introduces some additional network latency, which may be significant in high-performance applications.

5. **Polling and Scraping**
    - **Description**: This method involves periodically querying or scraping services for metrics or logs, typically using tools like Prometheus that pull data from endpoints exposed by the services.
    - **Pros**:
        - **Low Intrusion**: Polling allows data collection without modifying the application or deploying additional components (like agents or sidecars).
        - **Simplicity**: This method is easy to set up and manage, especially for collecting metrics at regular intervals.
        - **Centralized Control**: A central system (like Prometheus) manages all data collection, simplifying configuration.
    - **Cons**:
        - **Limited Granularity**: Polling intervals may miss short-lived events or rapid fluctuations in performance.
        - **Increased Load**: Frequent polling can put a load on the services being monitored, potentially affecting their performance.
        - **Latency**: Data may not be available in real-time due to the periodic nature of polling, leading to delays in detecting issues.

Each method of collecting telemetry data has its own set of advantages and trade-offs, and the choice often depends on the specific requirements and constraints of the system being monitored. In practice, a combination of these methods is often used to achieve comprehensive observability.

## References
* chatgpt
* udemy - Metric and Log Collection with Agents, New Relic Query Language (NRQL), Alerts and Incidents, and New Relic CLI