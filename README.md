[comment]: # "Auto-generated SOAR connector documentation"
# McAfee Web Gateway

Publisher: Splunk Community  
Connector Version: 1\.0\.2  
Product Vendor: McAfee  
Product Name: McAfee Web Gateway  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.9\.39220  

This app integrates with McAfee Web Gateway to perform contain and correct actions for maintaining lists

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2020 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
#### Setup

In order to set up an asset, you will need to first do the following on McAfee Web Gateway:

1.  [Enable the REST interface (Click HERE to go to McAfee
    documentation)](https://docs.mcafee.com/bundle/web-gateway-9.1.x-product-guide/page/GUID-F559827C-224E-49E8-AA5B-7D389EF39E4A.html)
2.  [Give permission to access (Click HERE to go to McAfee
    documentation)](https://docs.mcafee.com/bundle/web-gateway-9.1.x-product-guide/page/GUID-2D0D4E6C-E96A-4B52-8602-BF322B2AC914.html)

  
*Note: It is important to create a separate account for Splunk> Phantom to use since a user cannot
log in more than once at a time.*

#### Block/Unblock Actions

**block** actions (block url\|ip\|domain) *only* add items to a provided list. It is up to the
McAfee Web Gateway Administrators to manage the rules used for using that list in the correct rule.
**unblock** actions (unblock url\|ip\|domain) *only* remove items from a provided list. It is up to
the McAfee Web Gateway Administrators to manage the rules used for using that list in the correct
rule.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a McAfee Web Gateway asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Base URL \[Use port 4712 for https and 4711 for http\]
**verify\_server\_cert** |  optional  | boolean | Verify SSL
**username** |  required  | string | Username
**password** |  required  | password | Password

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[block url](#action-block-url) - Add URL to a list  
[unblock url](#action-unblock-url) - Remove URL from a list  
[block ip](#action-block-ip) - Add IP to a list  
[unblock ip](#action-unblock-ip) - Remove IP from a list  
[block domain](#action-block-domain) - Add domain to a list  
[unblock domain](#action-unblock-domain) - Remove a domain from a list  
[add entry](#action-add-entry) - Add an entry to a list  
[remove entry](#action-remove-entry) - Remove an entry from a list  
[list lists](#action-list-lists) - Returns the available lists  
[get list](#action-get-list) - Returns contents of a list  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'block url'
Add URL to a list

Type: **contain**  
Read only: **False**

Either 'list\_title' or 'list\_id' are required, but the 'list\_id' is faster and recommended \(if available\)\. <br> Note\: Only adds URL to a list and blocking only occurs if the list is added to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**url** |  required  | URL to block | string |  `url` 
**description** |  optional  | Description to add to the entry | string | 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 
**entry\_position** |  optional  | Position of the list to add the block entry | numeric |  `mcafee web gateway entry position` 
**complex** |  optional  | Complex entry, to include a category and specify a protocol | boolean | 
**category** |  optional  | Category \(complex entry only\) | string | 
**protocol** |  optional  | Protocol \(complex entry only\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.category | string | 
action\_result\.parameter\.complex | boolean | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.protocol | string | 
action\_result\.parameter\.url | string |  `url` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `url` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'unblock url'
Remove URL from a list

Type: **correct**  
Read only: **False**

Either 'entry\_position' or 'url' is required, but the 'entry\_position' is faster and recommended \(if available\)\. <br> Note\: Only removes URL from a list and unblocking only occurs if the list is assigned to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**url** |  optional  | URL to unblock \(either 'url' or 'entry\_position' are required\) | string |  `url` 
**entry\_position** |  optional  | Position of the list entry to remove from the list | numeric |  `mcafee web gateway entry position` 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.url | string |  `url` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `url` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'block ip'
Add IP to a list

Type: **contain**  
Read only: **False**

Either 'list\_title' or 'list\_id' is required, but the 'list\_id' is faster and recommended \(if available\)\. <br> Note\: Only adds IP to a list and blocking only occurs if the list is added to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ip** |  required  | IP to block | string |  `ip` 
**description** |  optional  | Description to add to the entry | string | 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 
**entry\_position** |  optional  | Position of the list to add the block entry | numeric |  `mcafee web gateway entry position` 
**complex** |  optional  | Complex entry, to include a category and specify a protocol | boolean | 
**category** |  optional  | Category \(complex entry only\) | string | 
**protocol** |  optional  | Protocol \(complex entry only\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.category | string | 
action\_result\.parameter\.complex | boolean | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.protocol | string | 
action\_result\.parameter\.ip | string |  `ip` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `ip` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'unblock ip'
Remove IP from a list

Type: **correct**  
Read only: **False**

Either 'entry\_position' or 'ip' is required, but the 'entry\_position' is faster and recommended \(if available\)\. <br> Note\: Only removes IP from a list and unblocking only occurs if the list is assigned to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**ip** |  optional  | IP to unblock \(either 'ip' or 'entry\_position' are required\) | string |  `ip` 
**entry\_position** |  optional  | Position of the list entry to remove from the list | numeric |  `mcafee web gateway entry position` 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.ip | string |  `ip` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `ip` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'block domain'
Add domain to a list

Type: **contain**  
Read only: **False**

Either 'list\_title' or 'list\_id' is required, but the 'list\_id' is faster and recommended \(if available\)\. <br> Note\: Only adds domain to a list and blocking only occurs if the list is added to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  required  | Domain to block | string |  `domain` 
**description** |  optional  | Description to add to the entry | string | 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 
**entry\_position** |  optional  | Position of the list to add the block entry | numeric |  `mcafee web gateway entry position` 
**complex** |  optional  | Complex entry, to include a category and specify a protocol | boolean | 
**category** |  optional  | Category \(complex entry only\) | string | 
**protocol** |  optional  | Protocol \(complex entry only\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.category | string | 
action\_result\.parameter\.complex | boolean | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.protocol | string | 
action\_result\.parameter\.domain | string |  `domain` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `domain` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'unblock domain'
Remove a domain from a list

Type: **correct**  
Read only: **False**

Either 'entry\_position' or 'domain' is required, but the 'entry\_position' is faster and recommended \(if available\)\. <br> Note\: Only removes domain from a list and unblocking only occurs if the list is assigned to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**domain** |  optional  | Domain to unblock \(either 'domain' or 'entry\_position' are required\) | string |  `domain` 
**entry\_position** |  optional  | Position of the list entry to remove from the list | numeric |  `mcafee web gateway entry position` 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.domain | string |  `domain` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `domain` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add entry'
Add an entry to a list

Type: **contain**  
Read only: **False**

Either 'list\_title' or 'list\_id' is required, but the list\_id is faster and recommended \(if available\)\. <br> Note\: Only adds an entry to a list and blocking only occurs if the list is added to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**entry** |  required  | Entry to add | string |  `url`  `domain`  `ip`  `ip range` 
**description** |  optional  | Description to add to the entry | string | 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 
**entry\_position** |  optional  | Position of the list to add the block entry | numeric |  `mcafee web gateway entry position` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.description | string | 
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.entry | string |  `url`  `domain`  `ip`  `ip range` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `url`  `domain`  `ip`  `ip range` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'remove entry'
Remove an entry from a list

Type: **correct**  
Read only: **False**

Either 'entry\_position' or item are required, but the 'entry\_position' is faster and recommended \(if available\)\. <br> Note\: Only removes an entry from a list and unblocking only occurs if the list is assigned to a rule on McAfee Web Gateway\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**entry** |  optional  | Entry to remove \(either 'entry' or 'entry\_position' are required\) | string |  `url`  `domain`  `ip`  `ip range` 
**entry\_position** |  optional  | Position of the list entry to remove from the list | numeric |  `mcafee web gateway entry position` 
**list\_title** |  optional  | List Title \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID \(either 'list\_title' or 'list\_id' are required\) | string |  `mcafee web gateway list id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.parameter\.entry | string |  `url`  `domain`  `ip`  `ip range` 
action\_result\.data\.\*\.entry\.content\.listEntry\.entry | string |  `url`  `domain`  `ip`  `ip range` 
action\_result\.data\.\*\.entry\.content\.listEntry\.description | string | 
action\_result\.data\.\*\.entry\.id | string |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry\.title | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list lists'
Returns the available lists

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  optional  | List Type | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.type | string | 
action\_result\.data\.\*\.id | string |  `mcafee web gateway list id` 
action\_result\.data\.\*\.title | string |  `mcafee web gateway list title` 
action\_result\.data\.\*\.listType | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.lists\_found | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get list'
Returns contents of a list

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**list\_title** |  optional  | List Title | string |  `mcafee web gateway list title` 
**list\_id** |  optional  | List ID | string |  `mcafee web gateway list id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.list\_id | string |  `mcafee web gateway list id` 
action\_result\.parameter\.list\_title | string |  `mcafee web gateway list title` 
action\_result\.data\.\*\.description | string | 
action\_result\.data\.\*\.entry\_position | numeric |  `mcafee web gateway entry position` 
action\_result\.data\.\*\.entry | string |  `url`  `domain`  `ip`  `ip range` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.classifier | string | 
action\_result\.summary\.defaultRights | string | 
action\_result\.summary\.description | string | 
action\_result\.summary\.id | string |  `mcafee web gateway list id` 
action\_result\.summary\.list\_entries | numeric | 
action\_result\.summary\.mwg\-version | string | 
action\_result\.summary\.name | string |  `mcafee web gateway list title` 
action\_result\.summary\.structuralList | string | 
action\_result\.summary\.systemList | string | 
action\_result\.summary\.typeId | string | 
action\_result\.summary\.version | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 