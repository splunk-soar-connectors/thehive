[comment]: # "Auto-generated SOAR connector documentation"
# TheHive

Publisher: Splunk  
Connector Version: 2\.1\.3  
Product Vendor: TheHive Project  
Product Name: TheHive  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.10\.0\.40961  

This app integrates with an instance of TheHive to perform ticketing actions

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2018-2022 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
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


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a TheHive asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Device URL to connect to including the port
**api\_key** |  required  | password | API Key
**verify\_server\_cert** |  optional  | boolean | Verify server certificate

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[create ticket](#action-create-ticket) - Create a ticket \(issue\)  
[get ticket](#action-get-ticket) - Get ticket \(issue\) information  
[update ticket](#action-update-ticket) - Update ticket \(issue\)  
[list tickets](#action-list-tickets) - List all tickets  
[create task](#action-create-task) - Create Task  
[search ticket](#action-search-ticket) - Search ticket  
[search task](#action-search-task) - Search task  
[update task](#action-update-task) - Update the task  
[create observable](#action-create-observable) - Creates an observable for the specified case  
[get observables](#action-get-observables) - Retrieve observables associated with a case  
[create task log](#action-create-task-log) - Create task log  

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
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.owner | string |  `thehive username` 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.important\_data | string | 
action\_result\.summary\.new\_case\_id | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get ticket'
Get ticket \(issue\) information

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket ID \(AWGxGFw138eA2eAzW\_e6\) | string |  `thehive ticket id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
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
action\_result\.data\.\*\.resolutionStatus | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.summary | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
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
action\_result\.data\.\*\.flag | boolean | 
action\_result\.data\.\*\.id | string |  `thehive ticket id` 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.severity | numeric | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.tlp | numeric | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
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
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_tickets | numeric | 
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
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'search ticket'
Search ticket

Type: **generic**  
Read only: **False**

For example, \{"query"\: \{"\_in"\: \{"\_field"\: "title", "\_values"\: \["bill"\]\}\}\}<br>Note\: "\_values" field should be in lowercase only\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search\_ticket** |  required  | Search string | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
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
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.num\_results | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'search task'
Search task

Type: **generic**  
Read only: **False**

For example, \{"query"\: \{"\_in"\: \{"\_field"\: "title", "\_values"\: \["bill"\]\}\}\}<br>Note\: "\_values" field should be in lowercase only\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**search\_task** |  required  | Search string | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
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
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.num\_results | numeric | 
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
action\_result\.data\.\*\.id | string |  `thehive task id` 
action\_result\.data\.\*\.order | numeric | 
action\_result\.data\.\*\.owner | string | 
action\_result\.data\.\*\.startDate | numeric | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.title | string | 
action\_result\.data\.\*\.updatedAt | numeric | 
action\_result\.data\.\*\.updatedBy | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create observable'
Creates an observable for the specified case

Type: **generic**  
Read only: **False**

If a file is to be attached to this observable, the 'vault\_id' parameter must be used\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | Ticket ID \(ex\: AWGxGFw138eA2eAzW\_e6\) | string |  `thehive ticket id` 
**data\_type** |  required  | Data type of the observable \(select one from list\) | string | 
**data** |  optional  | Value of the data for this observable | string | 
**tlp** |  optional  | TLP \(default is Amber\) | string | 
**tags** |  required  | Tags to associate with this observable \(can be a comma\-separated list\) | string | 
**description** |  required  | Describe the observable in the context of the case | string | 
**vault\_id** |  optional  | Vault ID for the file to be attached\. Ignored if not 'file' data\_type | string |  `vault id` 
**ioc** |  optional  | Indicates if this observable is an IOC | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.data | string | 
action\_result\.parameter\.data\_type | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.id | string |  `thehive ticket id` 
action\_result\.parameter\.ioc | boolean | 
action\_result\.parameter\.tags | string | 
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
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
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
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
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
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 