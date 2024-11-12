# blacklens.io

The [blacklens.io](https://blacklens.io) integration allows you to monitor alerts. blacklens.io is a comprehensive Attack Surface Management platform that helps businesses understand and secure their external attack surface. By combining automated security analysis, continuous monitoring, and penetration testing, it identifies and addresses vulnerabilities early. With features like Darknet Monitoring, Vulnerability Scanning, and XDR Response, blacklens.io provides a proactive defense strategy to protect companies from cyber threats while offering a clear view of their security posture at all times.

Use the blacklens.io integration to fetch all related alerts about your Attack Surface. Then visualize that data in Kibana and create further alerts or enrich the data with other security solutions.

## Data streams

The blacklens.io integration collects one type of data streams: logs

**Alerts** returns a list of blacklens.io alerts (The API Docs are referenced within the portal)


## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it.
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.(You will require the 'alerts:read' Permission in order to fetch the Alerts via API

You need an active blacklens.io subscription and a user with the `alerts:read` permission to retrieve alerts via the API.

## Setup

### Copy blacklens.io required configuration properties

1. Login to your blacklens.io Portal (This URL will be used for the Instance URL: 'https://portal-(ID).blacklens.io')
2. Go to **Profile → Generate API Key** and copy it. 
3. Go to **Settings → Company**.
4. Copy **ws_id** and **tenant_id**.

### Enable the blacklens.io Integration in Elastic

1. In Kibana go to Management > Integrations.
2. In "Search for integrations" search bar, type blacklens.io.
3. Click on the "blacklens.io" integration from the search results.
4. Click on the "Add blacklens.io" button to add the integration.
5. Configure all required integration parameters. 
    - ARC data requires following parameters:
        - `URL`
        - `Tenant ID (tenant_id)`
        - `Workspace ID (ws_id)`
        - `API Key`
6. Save the integration.

For detailed setup instructions, please refer to the blacklens.io Knowledge Base (The link is referenced within the portal).

## Logs reference

### alerts

This is the `alerts` dataset

#### Example

An example event for `alerts` looks as following:

```json
{
    "_index": ".ds-logs-example.alerts-default-2024.11.07-000001",
    "_id": "exampleId12345=",
    "_version": 1,
    "_score": 0,
    "_source": {
        "input": {
            "type": "httpjson"
        },
        "agent": {
            "name": "example-agent",
            "id": "example-agent-id-12345",
            "type": "filebeat",
            "ephemeral_id": "ephemeral-id-12345",
            "version": "8.15.2"
        },
        "@timestamp": "2024-11-07T08:09:22.094Z",
        "ecs": {
            "version": "8.11.0"
        },
        "data_stream": {
            "namespace": "default",
            "type": "logs",
            "dataset": "example.alerts"
        },
        "elastic_agent": {
            "id": "example-agent-id-12345",
            "version": "8.15.2",
            "snapshot": false
        },
        "host": {
            "name": "example-host"
        },
        "blacklens": {
            "alert": {
                "severity": "info",
                "type_id": 1001,
                "details": [
                    {
                        "reference": "https://example.com/reference123",
                        "!cve": "CVE-2024-99999",
                        "#description": "An example vulnerability description with critical classification affecting a specific component.",
                        "Potential_affected_targets": [
                            "192.0.2.1:443",
                            "192.0.2.2:5001",
                            "192.0.2.3:5001",
                            "192.0.2.4:443"
                        ],
                        "CVSS_Score": 7.5
                    }
                ],
                "updated_date": "2024-08-14T15:06:13.151Z",
                "id": 12345,
                "type": "Example Threat System (ETS)",
                "title": "Example Threat Scan Notification",
                "outcome": "undefined",
                "status": "resolved"
            }
        },
        "message": "{\"affected_entities\":null,\"alert_outcome\":\"undefined\",\"alert_payload\":[{\"!cve\":\"CVE-2024-99999\",\"#description\":\"An example vulnerability description with critical classification affecting a specific component.\",\"CVSS_Score\":7.5,\"Potential_affected_targets\":[\"192.0.2.1:443\",\"192.0.2.2:5001\",\"192.0.2.3:5001\",\"192.0.2.4:443\"],\"reference\":\"https://example.com/reference123\"}],\"alert_status\":\"resolved\",\"created_date\":\"2024-11-07T08:09:22.094028Z\",\"customer_state\":\"open\",\"details\":{\"engine\":\"Example Threat System (ETS)\",\"id\":1001,\"title\":\"Example Threat Scan Notification\"},\"id\":12345,\"severity\":\"info\",\"type_id\":1001,\"updated_date\":\"2024-08-14T15:06:13.151728Z\"}",
        "event": {
            "agent_id_status": "verified",
            "ingested": "2024-11-07T09:45:30Z",
            "created": "2024-11-07T09:45:29.354Z",
            "kind": "alert",
            "category": [
                "threat"
            ],
            "type": [
                "info"
            ],
            "dataset": "example.alerts"
        },
        "tags": [
            "forwarded",
            "example-alert"
        ]
    },
    "fields": {
        "elastic_agent.version": [
            "8.15.2"
        ],
        "event.category": [
            "threat"
        ],
        "host.name.text": [
            "example-host"
        ],
        "blacklens.alert.type_id": [
            1001
        ],
        "agent.type": [
            "filebeat"
        ],
        "blacklens.alert.status": [
            "resolved"
        ],
        "blacklens.alert.outcome": [
            "undefined"
        ],
        "agent.name.text": [
            "example-agent"
        ],
        "blacklens.alert.type": [
            "Example Threat System (ETS)"
        ],
        "blacklens.alert.details.#description": [
            "An example vulnerability description with critical classification affecting a specific component."
        ],
        "agent.name": [
            "example-agent"
        ],
        "elastic_agent.snapshot": [
            false
        ],
        "host.name": [
            "example-host"
        ],
        "event.agent_id_status": [
            "verified"
        ],
        "event.kind": [
            "alert"
        ],
        "blacklens.alert.title": [
            "Example Threat Scan Notification"
        ],
        "blacklens.alert.details.!cve": [
            "CVE-2024-99999"
        ],
        "blacklens.alert.details.Potential_affected_targets": [
            "192.0.2.1:443",
            "192.0.2.2:5001",
            "192.0.2.3:5001",
            "192.0.2.4:443"
        ],
        "blacklens.alert.title.text": [
            "Example Threat Scan Notification"
        ],
        "elastic_agent.id": [
            "example-agent-id-12345"
        ],
        "data_stream.namespace": [
            "default"
        ],
        "input.type": [
            "httpjson"
        ],
        "blacklens.alert.details.reference": [
            "https://example.com/reference123"
        ],
        "blacklens.alert.severity": [
            "info"
        ],
        "message": [
            "{\"affected_entities\":null,\"alert_outcome\":\"undefined\",\"alert_payload\":[{\"!cve\":\"CVE-2024-99999\",\"#description\":\"An example vulnerability description with critical classification affecting a specific component.\",\"CVSS_Score\":7.5,\"Potential_affected_targets\":[\"192.0.2.1:443\",\"192.0.2.2:5001\",\"192.0.2.3:5001\",\"192.0.2.4:443\"],\"reference\":\"https://example.com/reference123\"}],\"alert_status\":\"resolved\",\"created_date\":\"2024-11-07T08:09:22.094028Z\",\"customer_state\":\"open\",\"details\":{\"engine\":\"Example Threat System (ETS)\",\"id\":1001,\"title\":\"Example Threat Scan Notification\"},\"id\":12345,\"severity\":\"info\",\"type_id\":1001,\"updated_date\":\"2024-08-14T15:06:13.151728Z\"}"
        ],
        "data_stream.type": [
            "logs"
        ],
        "tags": [
            "forwarded",
            "example-alert"
        ],
        "blacklens.alert.details.CVSS_Score": [
            7.5
        ],
        "blacklens.alert.updated_date": [
            "2024-08-14T15:06:13.151Z"
        ],
        "event.ingested": [
            "2024-11-07T09:45:30.000Z"
        ],
        "@timestamp": [
            "2024-11-07T08:09:22.094Z"
        ],
        "agent.id": [
            "example-agent-id-12345"
        ],
        "ecs.version": [
            "8.11.0"
        ],
        "blacklens.alert.id": [
            12345
        ],
        "data_stream.dataset": [
            "example.alerts"
        ],
        "event.created": [
            "2024-11-07T09:45:29.354Z"
        ],
        "event.type": [
            "indicator"
        ],
        "agent.ephemeral_id": [
            "ephemeral-id-12345"
        ],
        "agent.version": [
            "8.15.2"
        ],
        "event.dataset": [
            "example.alerts"
        ]
    }
}
```
**Exported fields**

| Field | Description | Type |
|---|---|---|
| @timestamp | Event timestamp. | date |
| blacklens.alert.details | Alert Details | nested |
| blacklens.alert.id | Unique Alert ID | integer |
| blacklens.alert.outcome | Determines whether the current alert triggers further events | keyword |
| blacklens.alert.severity | Alert Severity | keyword |
| blacklens.alert.status | Current Status of the Alert | keyword |
| blacklens.alert.title | Title/Description of the given Alert | keyword |
| blacklens.alert.type | Alert Type (Engine) | keyword |
| blacklens.alert.type_id | Alert Type ID (Engine) | integer |
| blacklens.alert.updated_date | Activity last updated time (UTC). | date |
| data_stream.dataset | Data stream dataset. | constant_keyword |
| data_stream.namespace | Data stream namespace. | constant_keyword |
| data_stream.type | Data stream type. | constant_keyword |
| event.dataset | Event dataset. | constant_keyword |
| event.kind |  | constant_keyword |
| event.module | Event module. | constant_keyword |
