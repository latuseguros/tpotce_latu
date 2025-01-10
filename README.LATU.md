# T-Pot - The All In One Multi Honeypot Platform - Latú

Primarily, a change was made to store the data generated in an AWS OpenSearch instance. The connection was established, and currently, the generated data is saved both in the tool's Elasticsearch and in our own OpenSearch. This provides the advantage of not being bound by data deletion policies.

## Logstash

Several changes were made to the `logstash.conf` file to connect to OpenSearch.

1. The output plugin for the connection to OpenSearch was installed (this was done in the Logstash Dockerfile).
2. The `docker-compose` was modified by adding a `docker-compose.override.yml` to update the Logstash service and apply the new changes directly from the specified Dockerfile.
3. Finally, connectivity tests were performed.

## Important Note for Deployment:

On certain Linux distributions, port 25 is already in use by default. To ensure proper functionality of tpot, you'll need to modify the `docker-compose.yml` file. Specifically, you'll want to comment out the line at position 424 (https://github.com/latuseguros/tpotce_latu/blob/40fa72dfed33bef0446670ce33ba7af687682d0b/docker-compose.yml#L424). This line is likely responsible for configuring port 25, which is causing a conflict with tpot.

By commenting out this line, you'll instruct Docker to ignore it and allow tpot to use port 25 without any issues.

## Improvements

- Note that the connection to OpenSearch was made using basic authentication; this should be improved to use specific IAM for the connection.
- Consider options for importing the Kibana Dashboard from Elasticsearch to OpenSearch Dashboard.
- Enhance security by implementing IAM roles for OpenSearch connections instead of basic authentication.
- Explore methods to migrate the Kibana Dashboard from Elasticsearch to the OpenSearch Dashboard.
- Evaluate the necessity of Elasticsearch/Kibana services and consider decommissioning them if redundant.
- Update the T-Pot web interface to integrate with our custom services.
