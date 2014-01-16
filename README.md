 
# API Specification: Credit repayments API 
 This document is the specification of a PayPal-as-a-Service Credit repayments API (see [﻿PayPal as a Service﻿](http://ppaas/)), conforming with the PPaaS API standards.
 
# Use Cases
The use cases supported by this API are:  
*  Retrieve all user bill payments.  
*  Retrieve details of an individual bill payment.  
*  Create a new bill payment.  
*  Update the schedule date, funding source information and payment amount of a bill payment that is not processed yet.  
*  Cancel an unprocessed bill payment.  
*  Processing a payment request generated from billpay. 
*  Retrieve the current constraints that apply for scheduling or updating an existing bill payment.  
*  Retrieve the current constraints that apply for configuring a user Credit account auto pay.  
*  Retrieve user auto pay configuration.  
*  Modify a user credit account auto pay configuration.  
*  Cancel a Credit account auto enrollment.  
*  Retrieve account bill payment overview of minimum due met, next auto pay amount and next auto pay date.  

# Domain model
*  [Model](https://confluence.paypal.com/cnfl/display/CREDITPD/GCE+-+Re-Payment+Resource+Model)
   
# Resources
This section describes the resources derived from the domain model. 
## [billpay](billpay.json)
### Description
Details about the Credit bill payment. The payment can be a one-off payment or generated from autopay configuration.
### Representation
[billpay.json](billpay.json)
### Methods
#### get
Obtain the credit billpay resource identified by the billpay_id for the given fp account id.
```
 GET v1/credit/accounts/{fp_account_id}/billpay/{billpay_id}
```  
Request: only path parameters  
Response: [billpay](billpay.json)  
  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>BILLPAY_NOT_FOUND</td>
        <td>The billpay id in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### list
Retrieves a list of credit billpay resources for the specified fp account id.
```
 GET v1/credit/accounts/{fp_account_id}/billpay
```  
Request: only path parameters  
Response: Array of [billpay](billpay.json)  
  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### create
Creates a new Credit billpay resource.  
```
 POST v1/credit/accounts/{fp_account_id}/billpay
```  
Request: [billpay_config](billpay_config.json)  
Response: [billpay](billpay.json)  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### update
Updates an existing Credit billpay schedule configuration.
```
 PUT v1/credit/accounts/{fp_account_id}/billpay/{billpay_id}/schedule
```  
Request: [billpay_config](billpay_config.json)  
Response: [billpay](billpay.json)  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay update request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>BILLPAY_NOT_FOUND</td>
        <td>The billpay id in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### cancel
Cancels an existing Credit billpay.  
```
 PUT v1/credit/accounts/{fp_account_id}/billpay/{billpay_id}/status
```  
Request: [billpay_status](billpay_status.json)  
Response: [billpay](billpay.json)  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay cancel request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>BILLPAY_NOT_FOUND</td>
        <td>The billpay id in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table> 

#### repay
A processing resource that fulfills a repayment schedule by calling PayPal Money system to generate the transaction as instructed in the payment request. This step is part of the overal Credit Repayment processing process as known as the Money Movement step performed by PayPal subsystem.  
```
 POST v1/credit/billpay/repay
```  
Request: [payment_request.json](payment_request.json)  
Response: [payment_response.json](payment_response.json)  
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay repay request has succeeded.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_PAYER_ID</td>
        <td>Payer ID is invalid.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>PAYER_NOT_FOUND</td>
        <td>Can not find the PayPal user account given the payer id.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>SCHEDULE_NOT_FOUND</td>
        <td>Can not find the schedule in Finprod given the payment request id for legacy schedule.</td>
    </tr>
    <tr>
        <td>422 Unprocessable Entity </td>
        <td>INSUFFICIENT_PAYPAL_BALANCE</td>
        <td>User's PayPal Balance is insufficient to cover the payment amount and there is no Band funding source to use as back up.</td>
    </tr>
    <tr>
        <td>422 Unprocessable Entity </td>
        <td>AUTHORIZATION_REJECT</td>
        <td>The credit card or debit card authorization is rejected by the issuing bank.</td>
    </tr>
    <tr>
        <td>422 Unprocessable Entity</td>
        <td>FULFILLMENT_RISK_REJECT</td>
        <td>PayPal transaction risk rejects the payment request.</td>
    </tr>
    <tr>
        <td>524 Timeout Occurred</td>
        <td>PLANNING_TIMEOUT</td>
        <td>The Planning call timeout to response with a plan.</td>
    </tr>
    <tr>
        <td>524 Timeout Occurred</td>
        <td>FULFILLMENT_TIMEOUT</td>
        <td>The Fulfillment call timeout to response with payment status.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table> 

## [billpay_constraints](billpay_constraints.json)
### Description
Represents current constraints on the Credit account for making or scheduling a bill payment.
### Representation
[billpay_constraints.json](billpay_constraints.json)
### Methods
#### get
Obtain the current constraints/options available to schedule a repayment. The response cannot be cached, it changes with time because the resource is acted upon by billing cycle time.  
```
 GET v1/credit/accounts/{fp_account_id}/billpay-constraints
```  
Request: only path parameters    
Response: [billpay_constraints](billpay_constraints.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay_constraints get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

## [autopay_constraints](autopay_constraints.json)
### Description
Represents available options for an account's autopay configuration
### Representation
[autopay_constraints.json](autopay_constraints.json)
### Methods
#### get
Obtain the current constraints/options available for autopay setup. The response cannot be cached, it changes with time because the resource is acted upon by billing cycle time and can change the effective time of the autopay.  
```
 GET v1/credit/accounts/{fp_account_id}/autopay-constraints
```  
Request: only path parameters    
Response: [autopay_constraints](autopay_constraints.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The autopay_constraints get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

## [autopay](autopay.json)
### Description
A configuration for facilitating payments against a payer's credit account each billing cycle.
### Representation
[autopay.json](autopay.json)
### Methods
#### get
Obtain the credit repayment autopay configurations. At any time there may be at most 2 autopay configurations for the user, one that is currently active and another that will become active at a future time.  
```
 GET v1/credit/accounts/{fp_account_id}/autopay
```  
Request: only path parameters    
Response: Array of [autopay](autopay.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The autopay get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### setup
Creates or updates the accounts autopay configuration. The update can result in the user have two autopay configurations based on the effective of the new autopay configuration.   
```
 POST v1/credit/accounts/{fp_account_id}/autopay/setup
```  
Request: [autopay](autopay.json)    
Response: Array of [autopay](autopay.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The autopay setup request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

#### cancel
Unenrolls the Credit account from autopay. The cancel can result in a autopay configuration that will become effective based on the billing cycle.  
This results in the response containing at most two autopay configurations for the user.  
```
 POST v1/credit/accounts/{fp_account_id}/autopay/cancel
```  
Request: only path parameters    
Response: Array of [autopay](autopay.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The autopay cancel request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>

## [billpay_summary](billpay_summary.json)
### Description
The bill payment summary for the current cycle. The summary will provide the high level details of a user's upcoming bill payments for this cycle.
### Representation
[billpay_summary.json](billpay_summary.json)
### Methods
#### get
Returns the Credit account's bill payment summary for the current cycle. The response identifies payment overview information like minimum due met and the next autopay information, it is not a summary of an individual bill pay. The response cannot be cached, it changes with time because the computed resource varies by billing cycle time.  
```
 GET v1/credit/accounts/{fp_account_id}/billpay-summary
```  
Request: only path parameters    
Response: [billpay_summary](billpay_summary.json)    
<table>
    <tr>
        <th>Response Code</th>
        <th>Name</th>
        <th>Reason</th>
    </tr>
    <tr>
        <td>200 OK</td>
        <td>OK</td>
        <td>The billpay summary get request has succeeded</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>ACCOUNT_TYPE_NOT_SUPPORTED</td>
        <td>The FinProd Account specified in the request is not supported for this operation.</td>
    </tr>
    <tr>
        <td>400 Bad Request</td>
        <td>INVALID_FPACCOUNT_ID</td>
        <td>The correct FinProd Account identifier is either a 22 character Account id or a 13 character VRR number.</td>
    </tr>
    <tr>
        <td>404 Not Found</td>
        <td>FPACCOUNT_NOT_FOUND</td>
        <td>The FinProd Account in the request is not found.</td>
    </tr>
    <tr>
        <td>403 Forbidden</td>
        <td>FPACCOUNT_NOT_ACCESSIBLE</td>
        <td>The actor in context does not have access to the FinProd Account.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>UNKNOWN_SERVICE_ERROR</td>
        <td>Unknown error during execution of 3rd party services.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>SERVICE_COMM_ERROR</td>
        <td>Failure communicating with downstream service.</td>
    </tr>
    <tr>
        <td>500 Internal Server Error</td>
        <td>INTERNAL_SERVICE_ERROR</td>
        <td>Service encountered an unexpected condition which prevented it from fulfilling the request.</td>
    </tr>
</table>
