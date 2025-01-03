### **What is the Elastic Stack?**
- **Definition**: An open-source collection of tools (Elasticsearch, Logstash, Kibana, and Beats) designed for real-time search, analysis, and visualization of log file data.
- **Key Components**:
    - **Elasticsearch**: A distributed, JSON-based search engine with RESTful APIs.
    - **Logstash**: Handles log collection, transformation, and transportation.
    - **Kibana**: Visualization and analytics tool for Elasticsearch.
    - **Beats**: Lightweight data shippers to forward logs/metrics to Logstash or Elasticsearch.



### **Elastic Stack Components**
1. **Elasticsearch**:
    - Stores, indexes, and queries data.
    - Powers analytics on processed log records.
2. **Logstash**:
    - **Input Processing**: Collects data from various sources.
    - **Transformation**: Modifies and enriches log records.
    - **Output**: Sends processed records to Elasticsearch.
3. **Kibana**:
    - Visualizes Elasticsearch data using charts, tables, and dashboards.
    - Simplifies understanding query results.
4. **Beats**:
    - Installed on remote systems to ship data to Logstash/Elasticsearch.
    - Configurations:
        - **Beats -> Logstash -> Elasticsearch -> Kibana**
        - **Beats -> Elasticsearch -> Kibana**



### **Elastic Stack as a SIEM Solution**
- **Usage**:
    - Collect and analyze security-related data (e.g., firewalls, IDS/IPS, endpoints).
    - Store and index data in Elasticsearch.
    - Visualize and create dashboards in Kibana for security event insights.
    - Perform correlations and threat detection using Elasticsearch queries.
- **Primary Tool for SOC Analysts**:
    - Kibana, for querying and visualization.



### **Kibana Query Language (KQL)**
- **Basic Syntax**:
    - Queries consist of `field:value` pairs.
    - Example: `event.code:4625` filters for Windows event code 4625 (failed login attempts).
- **Features**:
    1. **Free Text Search**:
        - Search across all fields without specifying a field name.
    2. **Logical Operators**:
        - `AND`, `OR`, `NOT`, and parentheses for grouping.
    3. **Comparison Operators**:
        - `:`, `:>`, `:>=`, `:<`, `:<=`, `:!`.
    4. **Wildcards/Regular Expressions**:
        - Example: `user.name:admin*` filters for usernames starting with "admin".
- **Example Query**:
    ```kql
    event.code:4625 AND winlog.event_data.SubStatus:0xC0000072 AND @timestamp >= "2023-03-03T00:00:00.000Z" AND @timestamp <= "2023-03-06T23:59:59.999Z"
    ```
    - Filters for failed login attempts on disabled accounts during a specified time range.



### **How to Identify Available Data in Kibana**
1. **Free Text Search in Discover**:
    - Explore data and identify fields.
    - Example: Search for "4625" to reveal `event.code`, `winlog.event_id`, `@timestamp`.
2. **Elastic Documentation**:
    - Resources for field identification:
        - Elastic Common Schema (ECS)
        - Winlogbeat and Filebeat fields.



### **Elastic Common Schema (ECS)**
- **Purpose**: A unified schema for event/log data across the Elastic Stack.
- **Advantages**:
    1. **Unified Data View**: Standardized fields for all data sources.
    2. **Efficient Search**: Easier query writing in KQL.
    3. **Enhanced Correlation**: Correlate events across sources.
    4. **Improved Visualizations**: Consistent dashboards and visual trends.
    5. **Elastic Interoperability**: Compatibility with Elastic solutions.
    6. **Future-proofing**: Ensures compatibility with new Elastic features.



### Questions
- Navigate to http://[Target IP]:5601, click on the side navigation toggle, and click on "Discover". Then, click on the calendar icon, specify "last 15 years", and click on "Apply". Finally, choose the "windows*" index pattern. Now, execute the KQL query that is mentioned in the "Comparison Operators" part of this section and enter the username of the disabled account as your answer. Just the username; no need to account for the domain.
	- anni
- Now, execute the KQL query that is mentioned in the "Wildcards and Regular Expressions" part of this section and enter the number of returned results (hits) as your answer.
	- 8