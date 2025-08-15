# TheHive

Publisher: Splunk <br>
Connector Version: 2.2.1 <br>
Product Vendor: TheHive Project <br>
Product Name: TheHive <br>
Minimum Product Version: 5.2.0

This app integrates with an instance of TheHive to perform ticketing actions

## Playbook Backward Compatibility

- The below-mentioned action has been added. Hence, it is requested to the end-user to please
  update their existing playbooks by inserting the corresponding action blocks for this action on
  the earlier versions of the app.

  - create task log

- The existing output data paths have been modified for the 'get observables' action. Hence, it is
  requested to the end-user to please update their existing playbooks by re-inserting | modifying
  | deleting the corresponding action blocks to ensure the correct functioning of the playbooks
  created on the earlier versions of the app.

Note: The asset configuration parameter 'timezone', will be used for the 'occur_date' parameter in
the 'add ttp' action.

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the TheHive server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http | tcp | 80 |
|         https | tcp | 443 |

### Configuration variables

This table lists the configuration variables required to operate TheHive. These variables are specified when configuring a TheHive asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base_url** | required | string | Device URL to connect to including the port |
**api_key** | required | password | API Key |
**verify_server_cert** | optional | boolean | Verify server certificate |
**timezone** | optional | timezone | Timezone (default: UTC) |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration <br>
[create ticket](#action-create-ticket) - Create a ticket (issue) <br>
[get ticket](#action-get-ticket) - Get ticket (issue) information <br>
[update ticket](#action-update-ticket) - Update ticket (issue) <br>
[list tickets](#action-list-tickets) - List all tickets <br>
[list alerts](#action-list-alerts) - List all alerts <br>
[create task](#action-create-task) - Create Task <br>
[search ticket](#action-search-ticket) - Search ticket <br>
[search task](#action-search-task) - Search task <br>
[update task](#action-update-task) - Update the task <br>
[create observable](#action-create-observable) - Creates an observable for the specified case/alert <br>
[get observables](#action-get-observables) - Retrieve observables associated with a case <br>
[create task log](#action-create-task-log) - Create task log <br>
[create alert](#action-create-alert) - Create Alert <br>
[get alert](#action-get-alert) - Get alert information <br>
[add ttp](#action-add-ttp) - Add TTP to Case

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied configuration

Type: **test** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'create ticket'

Create a ticket (issue)

Type: **generic** <br>
Read only: **False**

If the owner mentioned in the input parameter is an invalid user and it does not exist on The Hive platform, the ticket will get successfully created but, the owner displayed on the UI of The Hive will be \*\*\*unknown\*\*\* as per the API behavior. The user can update the same ticket by running the action Update Ticket with a valid user in the owner field.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**title** | required | Title | string | |
**description** | required | Description of the ticket | string | |
**severity** | optional | Severity of the case (default is Medium) | string | |
**tlp** | optional | TLP (default is Amber) | string | |
**owner** | optional | User to whom the case has been assigned (default is the user who created the case) | string | `thehive username` |
**fields** | optional | JSON containing field values | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.description | string | | testTicket |
action_result.parameter.fields | string | | {"field_name_1": "field_value_1", "field_name_2": "field_value_2"} |
action_result.parameter.owner | string | `thehive username` | test.user |
action_result.parameter.severity | string | | 3 |
action_result.parameter.title | string | | Test |
action_result.parameter.tlp | string | | White |
action_result.data.\*.\_id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_parent | string | | |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.caseId | numeric | `thehive case id` | 22 |
action_result.data.\*.createdAt | numeric | | 1519079897718 |
action_result.data.\*.createdBy | string | | testUser |
action_result.data.\*.description | string | | testTicket |
action_result.data.\*.endDate | numeric | | 1542187296341 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.impactStatus | string | | |
action_result.data.\*.owner | string | `thehive username` | test.user |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.resolutionStatus | string | | |
action_result.data.\*.severity | numeric | | 3 |
action_result.data.\*.startDate | numeric | | 1519079898453 |
action_result.data.\*.status | string | | Open |
action_result.data.\*.summary | string | | |
action_result.data.\*.title | string | | Test |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1542289085536 |
action_result.data.\*.updatedBy | string | | |
action_result.summary.important_data | string | | value |
action_result.summary.new_case_id | numeric | | 125 |
action_result.message | string | | Successfully created a new case |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get ticket'

Get ticket (issue) information

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Ticket ID | string | `thehive ticket id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `thehive ticket id` | AWGxGFw138eA2eAzW_e6 |
action_result.data.\*.\_id | string | `thehive ticket id` | AWGxGFw138eA2eAzW_e6 |
action_result.data.\*.\_parent | string | | |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.caseId | numeric | `thehive case id` | 31 |
action_result.data.\*.createdAt | numeric | | 1519094618881 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.customFields.incidentSource.order | numeric | | 2 |
action_result.data.\*.customFields.incidentSource.string | string | | User reported |
action_result.data.\*.customFields.viewer.order | numeric | | 1 |
action_result.data.\*.customFields.viewer.string | string | | |
action_result.data.\*.description | string | | testTicket |
action_result.data.\*.endDate | numeric | | 1542187296341 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.id | string | `thehive ticket id` | AWGxGFw138eA2eAzW_e6 |
action_result.data.\*.impactStatus | string | | NotApplicable |
action_result.data.\*.owner | string | `thehive username` | test.user |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.resolutionStatus | string | | Indeterminate |
action_result.data.\*.severity | numeric | | 3 |
action_result.data.\*.startDate | numeric | | 1519094619188 |
action_result.data.\*.status | string | | Open |
action_result.data.\*.summary | string | | Yes, plz close this |
action_result.data.\*.title | string | | Test |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1542289085536 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary | string | | |
action_result.message | string | | Successfully fetched ticket |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'update ticket'

Update ticket (issue)

Type: **generic** <br>
Read only: **False**

If the JSON containing fields is having invalid field names or invalid field values to update, then, none of the fields get updated and the action passes successfully.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Ticket ID | string | `thehive ticket id` |
**fields** | required | JSON containing field values | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.fields | string | | {"severity": 1, "description": "User, what are you doing"} |
action_result.parameter.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_parent | string | | |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case |
action_result.data.\*.\_version | numeric | | 2 |
action_result.data.\*.caseId | numeric | | 125 |
action_result.data.\*.createdAt | numeric | | 1529529092329 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.customFields.incidentSource.order | numeric | | 2 |
action_result.data.\*.customFields.incidentSource.string | string | | |
action_result.data.\*.customFields.test.order | numeric | | 3 |
action_result.data.\*.customFields.test.string | string | | 1 |
action_result.data.\*.customFields.viewer.order | numeric | | 1 |
action_result.data.\*.customFields.viewer.string | string | | Test |
action_result.data.\*.description | string | | User, what are you doing |
action_result.data.\*.endDate | numeric | | 1542187296341 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.impactStatus | string | | |
action_result.data.\*.owner | string | | testUser |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.resolutionStatus | string | | |
action_result.data.\*.severity | numeric | | 1 |
action_result.data.\*.startDate | numeric | | 1529529092817 |
action_result.data.\*.status | string | | Open |
action_result.data.\*.summary | string | | |
action_result.data.\*.title | string | | QA |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1529529095327 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary | string | | |
action_result.message | string | | Successfully updated ticket |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list tickets'

List all tickets

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.data.\*.\_id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_parent | string | | |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case |
action_result.data.\*.\_version | numeric | | 2 |
action_result.data.\*.caseId | numeric | | 73 |
action_result.data.\*.createdAt | numeric | | 1523913195723 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.customFields.incidentCategory.order | numeric | | 1 |
action_result.data.\*.customFields.incidentCategory.string | string | | |
action_result.data.\*.customFields.incidentSource.order | numeric | | 2 |
action_result.data.\*.customFields.incidentSource.string | string | | |
action_result.data.\*.customFields.incidentSourced.string | string | | User reported |
action_result.data.\*.customFields.test.order | numeric | | 1 |
action_result.data.\*.customFields.test.string | string | | 1 |
action_result.data.\*.customFields.viewer.order | numeric | | 1 |
action_result.data.\*.customFields.viewer.string | string | | Kartik |
action_result.data.\*.description | string | | Today is a beautiful day! |
action_result.data.\*.endDate | numeric | | 1542187296341 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.impactStatus | string | | NotApplicable |
action_result.data.\*.metrics.Impacted Users | numeric | | 1 |
action_result.data.\*.metrics.Metrics Test | numeric | | 5 |
action_result.data.\*.metrics.MetricsTest | numeric | | 5 |
action_result.data.\*.metrics.Recipients Test | numeric | | 5 |
action_result.data.\*.owner | string | `thehive username` | admin |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.resolutionStatus | string | | Indeterminate |
action_result.data.\*.severity | numeric | | 1 |
action_result.data.\*.startDate | numeric | | 1523913196534 |
action_result.data.\*.status | string | | Open |
action_result.data.\*.summary | string | | Yes, plz close this |
action_result.data.\*.tags | string | | Phishing |
action_result.data.\*.title | string | | Test |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1523912044312 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary | string | | |
action_result.summary.num_tickets | numeric | | 21 |
action_result.message | string | | Num tickets: 239 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list alerts'

List all alerts

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.data.\*.\_id | string | `thehive alert id` | ~557296 |
action_result.data.\*.\_type | string | | alert |
action_result.data.\*.artifacts.\*.\_id | string | | ~651296 |
action_result.data.\*.artifacts.\*.\_type | string | | case_artifact |
action_result.data.\*.artifacts.\*.attachment.contentType | string | | application/zip |
action_result.data.\*.artifacts.\*.attachment.hashes | string | `md5` | c2b8d2623a1fd062a898615015583ce9 |
action_result.data.\*.artifacts.\*.attachment.id | string | `sha256` | 1fcadb1293968b037bb0de3a8a6e8368cdf8ab7ab9718023abaa14d2a41f501b |
action_result.data.\*.artifacts.\*.attachment.name | string | | file_name.apk |
action_result.data.\*.artifacts.\*.attachment.size | numeric | | 1434318 |
action_result.data.\*.artifacts.\*.createdAt | numeric | | 1650452201934 |
action_result.data.\*.artifacts.\*.createdBy | string | `email` | adminuser@thehive.local |
action_result.data.\*.artifacts.\*.data | string | | 10.1.19.195 |
action_result.data.\*.artifacts.\*.dataType | string | | ip |
action_result.data.\*.artifacts.\*.id | string | | ~651296 |
action_result.data.\*.artifacts.\*.ioc | boolean | | True False |
action_result.data.\*.artifacts.\*.message | string | | Test artifact message |
action_result.data.\*.artifacts.\*.sighted | boolean | | True False |
action_result.data.\*.artifacts.\*.startDate | numeric | | 1650452201934 |
action_result.data.\*.artifacts.\*.tags | string | | domain |
action_result.data.\*.artifacts.\*.tlp | numeric | | 2 |
action_result.data.\*.case | string | | |
action_result.data.\*.caseTemplate | string | | TestCaseTemplateName |
action_result.data.\*.createdAt | numeric | | 1650451922582 |
action_result.data.\*.createdBy | string | `email` | adminuser@thehive.local |
action_result.data.\*.date | numeric | | 1650451922577 |
action_result.data.\*.description | string | | Alert description |
action_result.data.\*.externalLink | string | | |
action_result.data.\*.follow | boolean | | True False |
action_result.data.\*.id | string | `thehive alert id` | ~557296 |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.severity | numeric | | 2 |
action_result.data.\*.source | string | | Test App |
action_result.data.\*.sourceRef | string | | test_source_ref |
action_result.data.\*.status | string | | New |
action_result.data.\*.tags | string | | alert-automation |
action_result.data.\*.title | string | | Test Alert title |
action_result.data.\*.tlp | numeric | | 3 |
action_result.data.\*.type | string | | Test Event |
action_result.data.\*.updatedAt | string | | |
action_result.data.\*.updatedBy | string | | |
action_result.summary.num_alerts | numeric | | 12 |
action_result.message | string | | Num alerts: 12 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create task'

Create Task

Type: **generic** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Ticket ID | string | `thehive ticket id` |
**title** | required | Title | string | |
**status** | required | Status | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.parameter.status | string | | Waiting |
action_result.parameter.title | string | | The Waiting is the Hardest Part |
action_result.data.\*.\_id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.\_parent | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case_task |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.createdAt | numeric | | 1519157031533 |
action_result.data.\*.createdBy | string | | testUser |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.group | string | | default |
action_result.data.\*.id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.order | numeric | | 0 |
action_result.data.\*.status | string | | Waiting |
action_result.data.\*.title | string | | The Waiting is the Hardest Part |
action_result.summary | string | | |
action_result.message | string | | Successfully created task |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'search ticket'

Search ticket

Type: **generic** <br>
Read only: **False**

For example, {"\_in": {"\_field": "title", "\_values": ["bill"]}}<br>Note: "\_values" field should be in lowercase only.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search_ticket** | required | Search string | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.search_ticket | string | | {"\_in": {"\_field": "title", "\_values": ["test"]}} {"\_like": {"\_field": "title","\_value": "\*testing\*"}} {"\_lt": {"tlp": 3}} |
action_result.data.\*.\_id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_parent | string | | |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case |
action_result.data.\*.\_version | numeric | | 2 |
action_result.data.\*.caseId | numeric | `thehive case id` | 73 |
action_result.data.\*.createdAt | numeric | | 1523913195723 |
action_result.data.\*.createdBy | string | | testUser |
action_result.data.\*.customFields.incidentCategory.order | numeric | | 1 |
action_result.data.\*.customFields.incidentCategory.string | string | | |
action_result.data.\*.customFields.incidentSource.order | numeric | | 2 |
action_result.data.\*.customFields.incidentSource.string | string | | |
action_result.data.\*.customFields.incidentSourced.string | string | | User reported |
action_result.data.\*.customFields.test.order | numeric | | 3 |
action_result.data.\*.customFields.test.string | string | | 1 |
action_result.data.\*.customFields.viewer.order | numeric | | 1 |
action_result.data.\*.customFields.viewer.string | string | | Test |
action_result.data.\*.description | string | | User, what are you doing |
action_result.data.\*.endDate | numeric | | 1542187296341 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.id | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.impactStatus | string | | NotApplicable |
action_result.data.\*.metrics.Impacted Users | numeric | | 1 |
action_result.data.\*.metrics.Metrics Test | numeric | | 5 |
action_result.data.\*.metrics.MetricsTest | numeric | | 5 |
action_result.data.\*.metrics.Recipients Test | numeric | | 5 |
action_result.data.\*.owner | string | `thehive username` | admin |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.resolutionStatus | string | | Indeterminate |
action_result.data.\*.severity | numeric | | 1 |
action_result.data.\*.startDate | numeric | | 1523913196534 |
action_result.data.\*.status | string | | Open |
action_result.data.\*.string | string | | Yes, plz close this |
action_result.data.\*.summary | string | | Yes, plz close this |
action_result.data.\*.title | string | | Test |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1523913200583 |
action_result.data.\*.updatedBy | string | | testUser |
action_result.summary.num_results | numeric | | 10 |
action_result.message | string | | Num results: 10 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'search task'

Search task

Type: **generic** <br>
Read only: **False**

For example, {"\_in": {"\_field": "title", "\_values": ["bill"]}}<br>Note: "\_values" field should be in lowercase only.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search_task** | required | Search string | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.search_task | string | | {"\_in": {"\_field": "title", "\_values": ["test"]}} {"\_like": {"\_field": "title","\_value": "\*testing\*"}} {"\_lt": {"tlp": 3}} |
action_result.data.\*.\_id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.\_parent | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case_task |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.createdAt | numeric | | 1523913203133 |
action_result.data.\*.createdBy | string | | testUser |
action_result.data.\*.description | string | | This is for testing update task for InProgress status |
action_result.data.\*.endDate | numeric | | 1561129904827 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.group | string | | default |
action_result.data.\*.id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.order | numeric | | 0 |
action_result.data.\*.owner | string | | admin |
action_result.data.\*.startDate | numeric | | 1561129892485 |
action_result.data.\*.status | string | | Waiting |
action_result.data.\*.title | string | | Sorry folks, park's closed. Moose out front shoulda told ya |
action_result.data.\*.updatedAt | numeric | | 1561129904826 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary.num_results | numeric | | 10 |
action_result.message | string | | Num results: 10 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'update task'

Update the task

Type: **generic** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**task_id** | required | Task ID | string | `thehive task id` |
**task_title** | optional | Task title | string | |
**task_owner** | optional | Task owner | string | `thehive username` |
**task_status** | optional | Task status | string | |
**task_description** | optional | Task description | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.task_description | string | | Update |
action_result.parameter.task_id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.parameter.task_owner | string | `thehive username` | admin |
action_result.parameter.task_status | string | | Completed InProgress |
action_result.parameter.task_title | string | | The System updated the Name |
action_result.data.\*.\_id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.\_parent | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case_task |
action_result.data.\*.\_version | numeric | | 2 |
action_result.data.\*.createdAt | numeric | | 1520017954107 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.description | string | | Update |
action_result.data.\*.endDate | numeric | | 1520017956292 |
action_result.data.\*.flag | boolean | | True False |
action_result.data.\*.group | string | | default |
action_result.data.\*.id | string | `thehive task id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*.order | numeric | | 0 |
action_result.data.\*.owner | string | | admin |
action_result.data.\*.startDate | numeric | | 1542879276338 |
action_result.data.\*.status | string | | InProgress |
action_result.data.\*.title | string | | The System updated the Name |
action_result.data.\*.updatedAt | numeric | | 1520017956292 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary | string | | |
action_result.message | string | | Successfully updated task |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create observable'

Creates an observable for the specified case/alert

Type: **generic** <br>
Read only: **False**

If a file is to be attached to this observable, the 'vault_id' parameter must be used.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Ticket/Alert ID | string | `thehive ticket id` `thehive alert id` |
**ticket_type** | optional | Ticket or Alert (Default is Ticket) | string | |
**data_type** | required | Data type of the observable (select one from list) | string | |
**data** | optional | Value of the data for this observable | string | |
**tlp** | optional | TLP (default is Amber) | string | |
**tags** | optional | Tags to associate with this observable (can be a comma-separated list) | string | |
**description** | optional | Describe the observable in the context of the case | string | |
**vault_id** | optional | Vault ID for the file to be attached. Ignored if not 'file' data_type | string | `vault id` |
**ioc** | optional | Indicates if this observable is an IOC | boolean | |
**sighted** | optional | Indicates if this observable was sighted | boolean | |
**ignore_similarity** | optional | Indicates if this observable should be used or not to calculate the similarity stats | boolean | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.data | string | | http://www.test.com |
action_result.parameter.data_type | string | | domain |
action_result.parameter.description | string | | Testing with 2 different ticket id |
action_result.parameter.id | string | `thehive ticket id` `thehive alert id` | AWQfCdsmt-\_WVPphkhQv |
action_result.parameter.ignore_similarity | boolean | | False True |
action_result.parameter.ioc | boolean | | False True |
action_result.parameter.sighted | boolean | | False True |
action_result.parameter.tags | string | | domain |
action_result.parameter.ticket_type | string | | Ticket |
action_result.parameter.tlp | string | | Amber |
action_result.parameter.vault_id | string | `vault id` | 20f8d351f737e63e34c6d22794e6436421890ce1 |
action_result.data.\*.\_id | string | `thehive observable id` `md5` | 2e441ebe9994d5f6500454fbc10e148c |
action_result.data.\*.\_parent | string | `thehive ticket id` | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case_artifact |
action_result.data.\*.\_version | numeric | | 5 |
action_result.data.\*.attachment.contentType | string | | text/html |
action_result.data.\*.attachment.id | string | | cce34663afc32e28bcbf226c6e0f5fc21225651a13f3b0592a94b503b5dede8a |
action_result.data.\*.attachment.md5 | string | `md5` | 6ecf393fd38eebe6bdff0384c4b1e4d7 |
action_result.data.\*.attachment.name | string | | badfile.exe |
action_result.data.\*.attachment.sha1 | string | `sha1` | 201a6b3053cc1422d2c3670b62616331d2280929 |
action_result.data.\*.attachment.sha256 | string | `sha256` | 1cbec737f993e4922cee55cc2ebbfaafcd1cff8b790d8cfd2e6a5d550b648afa |
action_result.data.\*.attachment.size | numeric | | 14367 |
action_result.data.\*.createdAt | numeric | | 1520017954107 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.data | string | `url` | 122.122.122.122 |
action_result.data.\*.dataType | string | | domain |
action_result.data.\*.id | string | `thehive observable id` `md5` | 2e441ebe9994d5f6500454fbc10e148c |
action_result.data.\*.ioc | boolean | | True False |
action_result.data.\*.message | string | | Testing with 2 different ticket id |
action_result.data.\*.sighted | boolean | | True False |
action_result.data.\*.startDate | numeric | | 1520017954107 |
action_result.data.\*.status | string | | OK |
action_result.data.\*.tags | string | | domain |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.updatedAt | numeric | | 1520017956292 |
action_result.data.\*.updatedBy | string | | testUser |
action_result.summary | string | | |
action_result.message | string | | Successfully created observable |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get observables'

Retrieve observables associated with a case

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ticket_id** | required | Ticket ID to retrieve observables from | string | `thehive ticket id` |
**data_type** | optional | Limit the results by observable type | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.data_type | string | | fqdn domain file |
action_result.parameter.ticket_id | string | `thehive ticket id` | AWM8DPOUt-\_WVPphkhEG |
action_result.data.\*.\_id | string | `thehive observable id` `md5` | c898f24d96ecbbce9506f1b5260cf5bb |
action_result.data.\*.\_parent | string | `thehive ticket id` | AWM8DPOUt-\_WVPphkhEG |
action_result.data.\*.\_routing | string | | AWM8DPOUt-\_WVPphkhEG |
action_result.data.\*.\_type | string | | case_artifact |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.attachment.contentType | string | | application/msword |
action_result.data.\*.attachment.hashes | string | `md5` | 0a50c51731e49723e563babc54b6b404 |
action_result.data.\*.attachment.id | string | `sha256` | 0792bb710556be0218e669b31b94ee01ae639f36b504d4ca01b484918040ffca |
action_result.data.\*.attachment.md5 | string | `hash` `md5` | 0a50c51731e49723e563babc54b6b404 |
action_result.data.\*.attachment.name | string | | test.docx |
action_result.data.\*.attachment.sha1 | string | `hash` `sha1` | 20f8d351f737e63e34c6d22794e6436421890ce1 |
action_result.data.\*.attachment.sha256 | string | `hash` `sha256` | 0792bb710556be0218e669b31b94ee01ae639f36b504d4ca01b484918040ffca |
action_result.data.\*.attachment.size | numeric | | 11745 |
action_result.data.\*.createdAt | numeric | | 1534787641225 |
action_result.data.\*.createdBy | string | | admin |
action_result.data.\*.data | string | `url` | This is for testing purpose |
action_result.data.\*.dataType | string | | domain |
action_result.data.\*.id | string | `thehive observable id` `md5` | 1e3ca6553ce39d7e02bd33d810bc146f c898f24d96ecbbce9506f1b5260cf5bb |
action_result.data.\*.ioc | boolean | | True False |
action_result.data.\*.message | string | | This is for testing purpose Testing - domain |
action_result.data.\*.parent | string | `thehive ticket id` | AWM8DPOUt-\_WVPphkhEG |
action_result.data.\*.reports.Abuse_Finder_2_0.taxonomies.\*.level | string | | info |
action_result.data.\*.reports.Abuse_Finder_2_0.taxonomies.\*.namespace | string | | Abuse_Finder |
action_result.data.\*.reports.Abuse_Finder_2_0.taxonomies.\*.predicate | string | | Address |
action_result.data.\*.reports.Abuse_Finder_2_0.taxonomies.\*.value | string | `email` | xyz@test.com |
action_result.data.\*.sighted | boolean | | True False |
action_result.data.\*.startDate | numeric | | 1534787641306 |
action_result.data.\*.status | string | | Deleted |
action_result.data.\*.tags | string | | domain |
action_result.data.\*.tlp | numeric | | 3 |
action_result.data.\*.updatedAt | numeric | | 1542199783148 |
action_result.data.\*.updatedBy | string | | admin |
action_result.summary | string | | |
action_result.message | string | | Num observables found: 8 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create task log'

Create task log

Type: **generic** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**task_id** | required | Task ID | string | `thehive task id` |
**message** | required | Message | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.message | string | | This is expected activity. Closing Task |
action_result.parameter.task_id | string | `thehive task id` | AZmubWXJkcm5LPGvTUh\_ |
action_result.data.\*.\_id | string | `thehive task log id` | AWQfCdsmt-\_WVPphkhQv |
action_result.data.\*._parent | string | `thehive task id` | AZmubWXJkcm5LPGvTUh_ |
action_result.data.\*.\_routing | string | | AWQfCcret-\_WVPphkhQq |
action_result.data.\*.\_type | string | | case_task_log |
action_result.data.\*.\_version | numeric | | 1 |
action_result.data.\*.createdAt | numeric | | 1519157031533 |
action_result.data.\*.createdBy | string | | testUser |
action_result.data.\*.id | string | `thehive task log id` | AWG00LJx38eA2eAzW_gL |
action_result.data.\*.message | string | | This is expected activity. Closing Task |
action_result.data.\*.order | numeric | | 0 |
action_result.data.\*.owner | string | | username |
action_result.data.\*.startDate | numeric | | 1631792756852 |
action_result.data.\*.status | string | | Waiting |
action_result.summary | string | | |
action_result.message | string | | Successfully created task log |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create alert'

Create Alert

Type: **generic** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**title** | required | Title | string | |
**description** | required | Description | string | |
**severity** | optional | Severity of the alert (default is Medium) | string | |
**tags** | optional | Tags to associate with this alert (can be a comma-separated list) | string | |
**tlp** | optional | TLP (default is Amber) | string | |
**type** | required | Type of the alert | string | |
**source** | required | Source of the alert | string | |
**source_ref** | required | Source reference of the alert | string | |
**artifacts** | optional | JSON Array containing artifact attributes | string | |
**case_template** | optional | Case template to use when case is created from this alert | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.artifacts | string | | \[{"dataType":"mail", "tags":["Recipient"], "data":["testuser@domain.com"]}\] |
action_result.parameter.case_template | string | | TemplateName |
action_result.parameter.description | string | | Alert description text |
action_result.parameter.severity | string | | Medium |
action_result.parameter.source | string | | Cofense Add-on |
action_result.parameter.source_ref | string | | 2272 |
action_result.parameter.tags | string | | phishing |
action_result.parameter.title | string | | This is a test from App With Observables |
action_result.parameter.tlp | string | | Amber |
action_result.parameter.type | string | | internal |
action_result.data.\*.\_id | string | `thehive alert id` | ~32800 |
action_result.data.\*.\_type | string | | alert |
action_result.data.\*.artifacts.\*.\_id | string | | ~57520 |
action_result.data.\*.artifacts.\*.\_type | string | | case_artifact |
action_result.data.\*.artifacts.\*.createdAt | numeric | | 1649779088314 |
action_result.data.\*.artifacts.\*.createdBy | string | `email` | user@domain.com |
action_result.data.\*.artifacts.\*.data | string | `email` | testuser@domain.edu |
action_result.data.\*.artifacts.\*.dataType | string | | mail |
action_result.data.\*.artifacts.\*.id | string | | ~57520 |
action_result.data.\*.artifacts.\*.ioc | boolean | | True False |
action_result.data.\*.artifacts.\*.message | string | | This is example message |
action_result.data.\*.artifacts.\*.sighted | boolean | | True False |
action_result.data.\*.artifacts.\*.startDate | numeric | | 1649779088314 |
action_result.data.\*.artifacts.\*.tags | string | | Recipient |
action_result.data.\*.artifacts.\*.tlp | numeric | | 2 |
action_result.data.\*.case | string | | |
action_result.data.\*.caseTemplate | string | | |
action_result.data.\*.createdAt | numeric | | 1649779088308 |
action_result.data.\*.createdBy | string | `email` | user@domain.com |
action_result.data.\*.date | numeric | | 1649779088305 |
action_result.data.\*.description | string | | Alert description text |
action_result.data.\*.externalLink | string | | |
action_result.data.\*.follow | boolean | | True False |
action_result.data.\*.id | string | `thehive alert id` | ~32800 |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.severity | numeric | | 2 |
action_result.data.\*.source | string | | Cofense Add-on |
action_result.data.\*.sourceRef | string | | 2272 |
action_result.data.\*.status | string | | New |
action_result.data.\*.tags | string | | phishing |
action_result.data.\*.title | string | | This is a test from App With Observables |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.type | string | | internal |
action_result.data.\*.updatedAt | string | | |
action_result.data.\*.updatedBy | string | | |
action_result.summary | string | | |
action_result.message | string | | Successfully created task |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get alert'

Get alert information

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Alert ID | string | `thehive alert id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `thehive alert id` | ~32968 |
action_result.data.\*.\_id | string | `thehive alert id` | ~32968 |
action_result.data.\*.\_type | string | | alert |
action_result.data.\*.artifacts.\*.\_id | string | | ~786632 |
action_result.data.\*.artifacts.\*.\_type | string | | case_artifact |
action_result.data.\*.artifacts.\*.createdAt | numeric | | 1650522468968 |
action_result.data.\*.artifacts.\*.createdBy | string | | testuser@domain.local |
action_result.data.\*.artifacts.\*.data | string | | http://www.somedomain.com |
action_result.data.\*.artifacts.\*.dataType | string | | domain |
action_result.data.\*.artifacts.\*.id | string | | ~786632 |
action_result.data.\*.artifacts.\*.ioc | boolean | | False |
action_result.data.\*.artifacts.\*.message | string | | This is test message |
action_result.data.\*.artifacts.\*.sighted | boolean | | False |
action_result.data.\*.artifacts.\*.startDate | numeric | | 1650522468968 |
action_result.data.\*.artifacts.\*.tlp | numeric | | 2 |
action_result.data.\*.case | string | | ~37056 |
action_result.data.\*.caseTemplate | string | | |
action_result.data.\*.createdAt | numeric | | 1649779406227 |
action_result.data.\*.createdBy | string | `email` | user@domain.com |
action_result.data.\*.date | numeric | | 1649779406223 |
action_result.data.\*.description | string | | Example description |
action_result.data.\*.externalLink | string | | |
action_result.data.\*.follow | boolean | | True False |
action_result.data.\*.id | string | `thehive alert id` | ~32968 |
action_result.data.\*.pap | numeric | | 2 |
action_result.data.\*.severity | numeric | | 2 |
action_result.data.\*.source | string | | Cofense Add-on |
action_result.data.\*.sourceRef | string | | 2271 |
action_result.data.\*.status | string | | Imported |
action_result.data.\*.tags | string | | phishing |
action_result.data.\*.title | string | | This is a test from App With Observables |
action_result.data.\*.tlp | numeric | | 2 |
action_result.data.\*.type | string | | internal |
action_result.data.\*.updatedAt | numeric | | 1649783209002 |
action_result.data.\*.updatedBy | string | `email` | user@domain.com |
action_result.summary | string | | |
action_result.message | string | | Successfully fetched alert |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'add ttp'

Add TTP to Case

Type: **investigate** <br>
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | Case ID | string | `thehive ticket id` |
**tactic** | required | Tactic | string | |
**pattern_id** | required | Pattern ID (Technique) | string | |
**occur_date** | optional | Occur Date (format: DD-MM-YYYY hh:mm) | string | |
**description** | optional | Procedure | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.description | string | | Test procedure |
action_result.parameter.id | string | `thehive ticket id` | ~73904 |
action_result.parameter.occur_date | string | | 17-04-2022 11:20 |
action_result.parameter.pattern_id | string | | T1566 |
action_result.parameter.tactic | string | | initial-access |
action_result.data.\*.\_createdAt | numeric | | 1649801936613 |
action_result.data.\*.\_createdBy | string | `email` | user@domain.com |
action_result.data.\*.\_id | string | | ~376864 |
action_result.data.\*.description | string | | Test Procedure |
action_result.data.\*.occurDate | numeric | | 1649801935925 |
action_result.data.\*.patternId | string | | T1566 |
action_result.data.\*.tactic | string | | initial-access |
action_result.summary | string | | |
action_result.message | string | | Successfully added tactic/technique |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |
action_result.parameter.ph | ph | | |

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2025 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
