[comment]: # "Auto-generated SOAR connector documentation"
# TheHive

Publisher: Splunk  
Connector Version: 2\.2\.0  
Product Vendor: TheHive Project  
Product Name: TheHive  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.2\.0  

This app integrates with an instance of TheHive to perform ticketing actions

[comment]: # " File: README.md"
[comment]: # "Copyright (c) 2018-2022 Splunk Inc."
[comment]: # ""
[comment]: # "Licensed under the Apache License, Version 2.0 (the 'License');"
[comment]: # "you may not use this file except in compliance with the License."
[comment]: # "You may obtain a copy of the License at"
[comment]: # ""
[comment]: # "    http://www.apache.org/licenses/LICENSE-2.0"
[comment]: # ""
[comment]: # "Unless required by applicable law or agreed to in writing, software distributed under"
[comment]: # "the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,"
[comment]: # "either express or implied. See the License for the specific language governing permissions"
[comment]: # "and limitations under the License."
[comment]: # ""
## Playbook Backward Compatibility

-   The below-mentioned action has been added. Hence, it is requested to the end-user to please
    update their existing playbooks by inserting the corresponding action blocks for this action on
    the earlier versions of the app.

      

    -   create task log

-   The existing output data paths have been modified for the 'get observables' action. Hence, it is
    requested to the end-user to please update their existing playbooks by re-inserting \| modifying
    \| deleting the corresponding action blocks to ensure the correct functioning of the playbooks
    created on the earlier versions of the app.

Note: The asset configuration parameter 'timezone', will be used for the 'occur_date' parameter in
the 'add ttp' action.

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the TheHive server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http         | tcp                | 80   |
|         https        | tcp                | 443  |


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a TheHive asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Device URL to connect to including the port
**api\_key** |  required  | password | API Key
**verify\_server\_cert** |  optional  | boolean | Verify server certificate
**timezone** |  optional  | timezone | Timezone \(default\: UTC\)

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[create ticket](#action-create-ticket) - Create a ticket \(issue\)  
[get ticket](#action-get-ticket) - Get ticket \(issue\) information  
[update ticket](#action-update-ticket) - Update ticket \(issue\)  
[list tickets](#action-list-tickets) - List all tickets  
[list alerts](#action-list-alerts) - List all alerts  
[create task](#action-create-task) - Create Task  
[search ticket](#action-search-ticket) - Search ticket  
[search task](#action-search-task) - Search task  
[update task](#action-update-task) - Update the task  
[create observable](#action-create-observable) - Creates an observable for the specified case/alert  
[get observables](#action-get-observables) - Retrieve observables associated with a case  
[create task log](#action-create-task-log) - Create task log  
[create alert](#action-create-alert) - Create Alert  
[get alert](#action-get-alert) - Get alert information  
[add ttp](#action-add-ttp) - Add TTP to Case  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'create ticket'
Create a ticket \(issue\)

Type: **generic**  
Read only: **False**

If the owner mentioned in the input parameter is an invalid user and it does not exist on The Hive platform, the ticket will get successfully created but, the owner displayed on the UI of The Hive will be \*\*\*unknown\*\*\* as per the API behavior\. The user can update the same ticket by running the action Update Ticket with a valid user in the owner field\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**title** |  required  | Title | string | 
**description** |  required  | Description of the ticket | string | 
**severity** |  optional  | Severity of the case \(default is Medium\) | string | 
**tlp** |  optional  | TLP \(default is Amber\) | string | 
**owner** |  optional  | User to whom the case has been assigned \(default is the user who created the case\) | string |  `thehive username` 
**fields** |  optional  | JSON containing field values | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.fields | string | 
action\_result\.parameter\.owner | string |  `thehive username` 
action\_result\.parameter\.severity | string | 
action\_result\.parameter\.title | string | 
action\_result\.parameter\.tlp | string | 
action\_result\.data\.\*\.\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_parent | string | 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.caseId | numeric |  `thehive case id` 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.impactStatus | string | 
action\_result\.data\.\*\.owner | string |  `thehive username` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary\.important\_data | string | 
action\_result\.summary\.new\_case\_id | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get ticket'
Get ticket \(issue\) information

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket ID | string |  `thehive ticket id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_parent | string | 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.caseId | numeric |  `thehive case id` 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.customFields\.incidentSource\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentSource\.string | string | 
action\_result\.data\.\*\.customFields\.viewer\.order | numeric | 
action\_result\.data\.\*\.customFields\.viewer\.string | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.impactStatus | string | 
action\_result\.data\.\*\.owner | string |  `thehive username` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'update ticket'
Update ticket \(issue\)

Type: **generic**  
Read only: **False**

If the JSON containing fields is having invalid field names or invalid field values to update, then, none of the fields get updated and the action passes successfully\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket ID | string |  `thehive ticket id` 
**fields** |  required  | JSON containing field values | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.fields | string | 
action\_result\.parameter\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_parent | string | 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.caseId | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.customFields\.incidentSource\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentSource\.string | string | 
action\_result\.data\.\*\.customFields\.test\.order | numeric | 
action\_result\.data\.\*\.customFields\.test\.string | string | 
action\_result\.data\.\*\.customFields\.viewer\.order | numeric | 
action\_result\.data\.\*\.customFields\.viewer\.string | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.impactStatus | string | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list tickets'
List all tickets

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.data\.\*\.\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_parent | string | 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.caseId | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.customFields\.incidentCategory\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentCategory\.string | string | 
action\_result\.data\.\*\.customFields\.incidentSource\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentSource\.string | string | 
action\_result\.data\.\*\.customFields\.incidentSourced\.string | string | 
action\_result\.data\.\*\.customFields\.test\.order | numeric | 
action\_result\.data\.\*\.customFields\.test\.string | string | 
action\_result\.data\.\*\.customFields\.viewer\.order | numeric | 
action\_result\.data\.\*\.customFields\.viewer\.string | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.impactStatus | string | 
action\_result\.data\.\*\.metrics\.Impacted Users | numeric | 
action\_result\.data\.\*\.metrics\.Metrics Test | numeric | 
action\_result\.data\.\*\.metrics\.MetricsTest | numeric | 
action\_result\.data\.\*\.metrics\.Recipients Test | numeric | 
action\_result\.data\.\*\.owner | string |  `thehive username` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_tickets | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list alerts'
List all alerts

Type: **investigate**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.data\.\*\.\_id | string |  `thehive alert id` 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_id | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.attachment\.contentType | string | 
action\_result\.data\.\*\.artifacts\.\*\.attachment\.hashes | string |  `md5` 
action\_result\.data\.\*\.artifacts\.\*\.attachment\.id | string |  `sha256` 
action\_result\.data\.\*\.artifacts\.\*\.attachment\.name | string | 
action\_result\.data\.\*\.artifacts\.\*\.attachment\.size | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.createdBy | string |  `email` 
action\_result\.data\.\*\.artifacts\.\*\.data | string | 
action\_result\.data\.\*\.artifacts\.\*\.dataType | string | 
action\_result\.data\.\*\.artifacts\.\*\.id | string | 
action\_result\.data\.\*\.artifacts\.\*\.ioc | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.message | string | 
action\_result\.data\.\*\.artifacts\.\*\.sighted | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.startDate | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.tags | string | 
action\_result\.data\.\*\.artifacts\.\*\.tlp | numeric | 
action\_result\.data\.\*\.case | string | 
action\_result\.data\.\*\.caseTemplate | string | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string |  `email` 
action\_result\.data\.\*\.date | numeric | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.externalLink | string | 
action\_result\.data\.\*\.follow | boolean | 
action\_result\.data\.\*\.id | string |  `thehive alert id` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.source | string | 
action\_result\.data\.\*\.sourceRef | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.updatedAt | string | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary\.num\_alerts | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create task'
Create Task

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket ID | string |  `thehive ticket id` 
**title** |  required  | Title | string | 
**status** |  required  | Status | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.id | string |  `thehive ticket id` 
action\_result\.parameter\.status | string | 
action\_result\.parameter\.title | string | 
action\_result\.data\.\*\.\_id | string |  `thehive task id` 
action\_result\.data\.\*\.\_parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.group | string | 
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'search ticket'
Search ticket

Type: **generic**  
Read only: **False**

For example, \{"\_in"\: \{"\_field"\: "title", "\_values"\: \["bill"\]\}\}<br>Note\: "\_values" field should be in lowercase only\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search\_ticket** |  required  | Search string | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.search\_ticket | string | 
action\_result\.data\.\*\.\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_parent | string | 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.caseId | numeric |  `thehive case id` 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.customFields\.incidentCategory\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentCategory\.string | string | 
action\_result\.data\.\*\.customFields\.incidentSource\.order | numeric | 
action\_result\.data\.\*\.customFields\.incidentSource\.string | string | 
action\_result\.data\.\*\.customFields\.incidentSourced\.string | string | 
action\_result\.data\.\*\.customFields\.test\.order | numeric | 
action\_result\.data\.\*\.customFields\.test\.string | string | 
action\_result\.data\.\*\.customFields\.viewer\.order | numeric | 
action\_result\.data\.\*\.customFields\.viewer\.string | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.impactStatus | string | 
action\_result\.data\.\*\.metrics\.Impacted Users | numeric | 
action\_result\.data\.\*\.metrics\.Metrics Test | numeric | 
action\_result\.data\.\*\.metrics\.MetricsTest | numeric | 
action\_result\.data\.\*\.metrics\.Recipients Test | numeric | 
action\_result\.data\.\*\.owner | string |  `thehive username` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.string | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary\.num\_results | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'search task'
Search task

Type: **generic**  
Read only: **False**

For example, \{"\_in"\: \{"\_field"\: "title", "\_values"\: \["bill"\]\}\}<br>Note\: "\_values" field should be in lowercase only\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search\_task** |  required  | Search string | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.search\_task | string | 
action\_result\.data\.\*\.\_id | string |  `thehive task id` 
action\_result\.data\.\*\.\_parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.group | string | 
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary\.num\_results | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'update task'
Update the task

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**task\_id** |  required  | Task ID | string |  `thehive task id` 
**task\_title** |  optional  | Task title | string | 
**task\_owner** |  optional  | Task owner | string |  `thehive username` 
**task\_status** |  optional  | Task status | string | 
**task\_description** |  optional  | Task description | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.task\_description | string | 
action\_result\.parameter\.task\_id | string |  `thehive task id` 
action\_result\.parameter\.task\_owner | string |  `thehive username` 
action\_result\.parameter\.task\_status | string | 
action\_result\.parameter\.task\_title | string | 
action\_result\.data\.\*\.\_id | string |  `thehive task id` 
action\_result\.data\.\*\.\_parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.endDate | numeric | 
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.group | string | 
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create observable'
Creates an observable for the specified case/alert

Type: **generic**  
Read only: **False**

If a file is to be attached to this observable, the 'vault\_id' parameter must be used\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket/Alert ID | string |  `thehive ticket id`  `thehive alert id` 
**ticket\_type** |  optional  | Ticket or Alert \(Default is Ticket\) | string | 
**data\_type** |  required  | Data type of the observable \(select one from list\) | string | 
**data** |  optional  | Value of the data for this observable | string | 
**tlp** |  optional  | TLP \(default is Amber\) | string | 
**tags** |  optional  | Tags to associate with this observable \(can be a comma\-separated list\) | string | 
**description** |  optional  | Describe the observable in the context of the case | string | 
**vault\_id** |  optional  | Vault ID for the file to be attached\. Ignored if not 'file' data\_type | string |  `vault id` 
**ioc** |  optional  | Indicates if this observable is an IOC | boolean | 
**sighted** |  optional  | Indicates if this observable was sighted | boolean | 
**ignore\_similarity** |  optional  | Indicates if this observable should be used or not to calculate the similarity stats | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.data | string | 
action\_result\.parameter\.data\_type | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.id | string |  `thehive ticket id`  `thehive alert id` 
action\_result\.parameter\.ignore\_similarity | boolean | 
action\_result\.parameter\.ioc | boolean | 
action\_result\.parameter\.sighted | boolean | 
action\_result\.parameter\.tags | string | 
action\_result\.parameter\.ticket\_type | string | 
action\_result\.parameter\.tlp | string | 
action\_result\.parameter\.vault\_id | string |  `vault id` 
action\_result\.data\.\*\.\_id | string |  `thehive observable id`  `md5` 
action\_result\.data\.\*\.\_parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.attachment\.contentType | string | 
action\_result\.data\.\*\.attachment\.id | string | 
action\_result\.data\.\*\.attachment\.md5 | string |  `md5` 
action\_result\.data\.\*\.attachment\.name | string | 
action\_result\.data\.\*\.attachment\.sha1 | string |  `sha1` 
action\_result\.data\.\*\.attachment\.sha256 | string |  `sha256` 
action\_result\.data\.\*\.attachment\.size | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.data | string |  `url` 
action\_result\.data\.\*\.dataType | string | 
action\_result\.data\.\*\.id | string |  `thehive observable id`  `md5` 
action\_result\.data\.\*\.ioc | boolean | 
action\_result\.data\.\*\.message | string | 
action\_result\.data\.\*\.sighted | boolean | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get observables'
Retrieve observables associated with a case

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ticket\_id** |  required  | Ticket ID to retrieve observables from | string |  `thehive ticket id` 
**data\_type** |  optional  | Limit the results by observable type | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.data\_type | string | 
action\_result\.parameter\.ticket\_id | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_id | string |  `thehive observable id`  `md5` 
action\_result\.data\.\*\.\_parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.attachment\.contentType | string | 
action\_result\.data\.\*\.attachment\.hashes | string |  `md5` 
action\_result\.data\.\*\.attachment\.id | string |  `sha256` 
action\_result\.data\.\*\.attachment\.md5 | string |  `hash`  `md5` 
action\_result\.data\.\*\.attachment\.name | string | 
action\_result\.data\.\*\.attachment\.sha1 | string |  `hash`  `sha1` 
action\_result\.data\.\*\.attachment\.sha256 | string |  `hash`  `sha256` 
action\_result\.data\.\*\.attachment\.size | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.data | string |  `url` 
action\_result\.data\.\*\.dataType | string | 
action\_result\.data\.\*\.id | string |  `thehive observable id`  `md5` 
action\_result\.data\.\*\.ioc | boolean | 
action\_result\.data\.\*\.message | string | 
action\_result\.data\.\*\.parent | string |  `thehive ticket id` 
action\_result\.data\.\*\.reports\.Abuse\_Finder\_2\_0\.taxonomies\.\*\.level | string | 
action\_result\.data\.\*\.reports\.Abuse\_Finder\_2\_0\.taxonomies\.\*\.namespace | string | 
action\_result\.data\.\*\.reports\.Abuse\_Finder\_2\_0\.taxonomies\.\*\.predicate | string | 
action\_result\.data\.\*\.reports\.Abuse\_Finder\_2\_0\.taxonomies\.\*\.value | string |  `email` 
action\_result\.data\.\*\.sighted | boolean | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create task log'
Create task log

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**task\_id** |  required  | Task ID | string |  `thehive task id` 
**message** |  required  | Message | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.message | string | 
action\_result\.parameter\.task\_id | string |  `thehive task id` 
action\_result\.data\.\*\.\_id | string |  `thehive task log id` 
action\_result\.data\.\*\.\_parent | string |  `thehive task id` 
action\_result\.data\.\*\.\_routing | string | 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.\_version | numeric | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string | 
action\_result\.data\.\*\.id | string |  `thehive task log id` 
action\_result\.data\.\*\.message | string | 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create alert'
Create Alert

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**title** |  required  | Title | string | 
**description** |  required  | Description | string | 
**severity** |  optional  | Severity of the alert \(default is Medium\) | string | 
**tags** |  optional  | Tags to associate with this alert \(can be a comma\-separated list\) | string | 
**tlp** |  optional  | TLP \(default is Amber\) | string | 
**type** |  required  | Type of the alert | string | 
**source** |  required  | Source of the alert | string | 
**source\_ref** |  required  | Source reference of the alert | string | 
**artifacts** |  optional  | JSON Array containing artifact attributes | string | 
**case\_template** |  optional  | Case template to use when case is created from this alert | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.artifacts | string | 
action\_result\.parameter\.case\_template | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.severity | string | 
action\_result\.parameter\.source | string | 
action\_result\.parameter\.source\_ref | string | 
action\_result\.parameter\.tags | string | 
action\_result\.parameter\.title | string | 
action\_result\.parameter\.tlp | string | 
action\_result\.parameter\.type | string | 
action\_result\.data\.\*\.\_id | string |  `thehive alert id` 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_id | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.createdBy | string |  `email` 
action\_result\.data\.\*\.artifacts\.\*\.data | string |  `email` 
action\_result\.data\.\*\.artifacts\.\*\.dataType | string | 
action\_result\.data\.\*\.artifacts\.\*\.id | string | 
action\_result\.data\.\*\.artifacts\.\*\.ioc | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.message | string | 
action\_result\.data\.\*\.artifacts\.\*\.sighted | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.startDate | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.tags | string | 
action\_result\.data\.\*\.artifacts\.\*\.tlp | numeric | 
action\_result\.data\.\*\.case | string | 
action\_result\.data\.\*\.caseTemplate | string | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string |  `email` 
action\_result\.data\.\*\.date | numeric | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.externalLink | string | 
action\_result\.data\.\*\.follow | boolean | 
action\_result\.data\.\*\.id | string |  `thehive alert id` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.source | string | 
action\_result\.data\.\*\.sourceRef | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.updatedAt | string | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get alert'
Get alert information

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Alert ID | string |  `thehive alert id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.id | string |  `thehive alert id` 
action\_result\.data\.\*\.\_id | string |  `thehive alert id` 
action\_result\.data\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_id | string | 
action\_result\.data\.\*\.artifacts\.\*\.\_type | string | 
action\_result\.data\.\*\.artifacts\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.createdBy | string | 
action\_result\.data\.\*\.artifacts\.\*\.data | string | 
action\_result\.data\.\*\.artifacts\.\*\.dataType | string | 
action\_result\.data\.\*\.artifacts\.\*\.id | string | 
action\_result\.data\.\*\.artifacts\.\*\.ioc | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.message | string | 
action\_result\.data\.\*\.artifacts\.\*\.sighted | boolean | 
action\_result\.data\.\*\.artifacts\.\*\.startDate | numeric | 
action\_result\.data\.\*\.artifacts\.\*\.tlp | numeric | 
action\_result\.data\.\*\.case | string | 
action\_result\.data\.\*\.caseTemplate | string | 
action\_result\.data\.\*\.createdAt | numeric | 
action\_result\.data\.\*\.createdBy | string |  `email` 
action\_result\.data\.\*\.date | numeric | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.externalLink | string | 
action\_result\.data\.\*\.follow | boolean | 
action\_result\.data\.\*\.id | string |  `thehive alert id` 
action\_result\.data\.\*\.pap | numeric | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.source | string | 
action\_result\.data\.\*\.sourceRef | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.tags | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string |  `email` 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add ttp'
Add TTP to Case

Type: **investigate**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Case ID | string |  `thehive ticket id` 
**tactic** |  required  | Tactic | string | 
**pattern\_id** |  required  | Pattern ID \(Technique\) | string | 
**occur\_date** |  optional  | Occur Date \(format\: DD\-MM\-YYYY hh\:mm\) | string | 
**description** |  optional  | Procedure | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.id | string |  `thehive ticket id` 
action\_result\.parameter\.occur\_date | string | 
action\_result\.parameter\.pattern\_id | string | 
action\_result\.parameter\.tactic | string | 
action\_result\.data\.\*\.\_createdAt | numeric | 
action\_result\.data\.\*\.\_createdBy | string |  `email` 
action\_result\.data\.\*\.\_id | string | 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.occurDate | numeric | 
action\_result\.data\.\*\.patternId | string | 
action\_result\.data\.\*\.tactic | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 