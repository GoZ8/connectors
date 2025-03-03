# OpenCTI Sentinel Connector
This OpenCTI connector allows the ability to create or delete data from your OpenCTI platform to either the Microsoft Sentinel or Microsoft Defender for Endpoint platform utitlizing the [Microsofot Graph API Threat Intelligence Indicator](https://learn.microsoft.com/en-us/graph/api/resources/tiindicator?view=graph-rest-beta). Microsoft has a detailed guide on how to get started with connecting your threat intellgience platform to Sentinel found [here](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/data/sentinel-threat-intelligence#import-threat-indicators-with-the-platforms-data-connector).

## Installation

### Requirements

- OpenCTI Platform >= 5.10.2

### Configuration

| Parameter                            | Docker envvar                       | Mandatory    | Description                                                                                                                                                |
| ------------------------------------ | ----------------------------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `opencti_url`                        | `OPENCTI_URL`                       | Yes          | The URL of the OpenCTI platform.                                                                                                                           |
| `opencti_token`                      | `OPENCTI_TOKEN`                     | Yes          | The default admin token configured in the OpenCTI platform parameters file.                                                                                |
| `connector_id`                       | `CONNECTOR_ID`                      | Yes          | A valid arbitrary `UUIDv4` that must be unique for this connector.                                                                                         |
| `connector_type`                     | `CONNECTOR_TYPE`                    | Yes          | Must be `STREAM` (this is the connector type).                                                                                                      |
| `connector_name`                     | `CONNECTOR_NAME`                    | Yes          | Must be `sentinel`, not used in this connector.                                                                                                                                         |
| `connector_scope`                    | `CONNECTOR_SCOPE`                   | Yes          | Must be `sentinel`, not used in this connector.                                                                                                 |
| `connector_confidence_level`         | `CONNECTOR_CONFIDENCE_LEVEL`        | Yes          | The default confidence level for created sightings (a number between 1 and 4).                                                                             |
| `connector_log_level`                | `CONNECTOR_LOG_LEVEL`               | Yes          | The log level for this connector, could be `debug`, `info`, `warn` or `error` (less verbose).                                                              |
| `tenant_id`                          | `TENANT_ID`                         | Yes          | Your Azure Tentent ID                                                                                                                                           |
| `client_id`                          | `CLIENT_ID`                         | Yes          | Your Azure App Client ID                                                                                                                                        |
| `client_secret`                      | `CLIENT_SECRET`                     | Yes          | Your Azure App Client Secret                                                                                                                                    |
| `login_url`                          | `LOGIN_URL`                         | Yes          | Login URL for Microsoft which is `https://login.microsoft.com`                                                                                                                                 |
| `resource_url`                       | `RESOURCE_URL`                      | Yes          | The resource the API will use which is `https://graph.microsoft.com`                                                                                                           |
| `request_url`                        | `REQUEST_URL`                       | Yes          | The request URL that will be used which is `/beta/security/tiIndicators`                                                                                                              |
| `confidence_level`                   | `CONFIDENCE_LEVEL`                  | Yes          | Alerts equal to or higher than this will be blocked, Lower will be alerted, and 0 will be allowed must be between 0 to 100                                                                                                                      |
| `expire_time`                        | `EXPIRE_TIME`                       | Yes          | Number of days for your indicator to expire in Sentinel. Suggestion of `30` as a default                                                         |
| `target_product`                     | `TARGET_PRODUCT`                    | Yes          | `Azure Sentinel` or `Microsoft Defender` ATP"                                                                                                               |
| `action`                             | `ACTION`                            | No           | The action to apply if the indicator is matched from within the targetProduct security tool. Possible values are: `unknown`, `allow`, `block`, `alert`.                                                                                                    |
| `tlp_level`                          | `TLP_LEVEL`                         | No           | This will overide all TLP values submitted to Sentinel to this. Possible TLP values are `unknown`, `white`, `green`, `amber`, `red`                                                 |
| `passiveOnly`                        | `PASSIVE_ONLY`                      | No           | Determines if the indicator should trigger an event that is visible to an end-user. When set to `True` security tools will not notify the end user that a ‘hit’ has occurred. This is most often treated as audit or silent mode by security products where they will simply log that a match occurred but will not perform the action. Default value is `False`.                                                                                                                       |



