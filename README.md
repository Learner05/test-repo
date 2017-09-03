# Payment Arrangements API

Services details for all future dated payment scenarios.

**Business Features:**<span class="business_feature"> #Autopay  #Direct Debit #ScheduledPayment #Care Payment #WebCollect Payment #Multiple Scheduled Payment #MSP #Monthly Payment #Weekly payment #Cycle Cut #NPDD</span>

**Version:** 1.0

**Contact information:**  
Enterprise Money Movement (EMM)  
gallagheraxpcrew@aexp.com  


**License:** American Express Technologies
## Create an Arrangement

> URL

```Any
POST https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements
```
> Header Params

```US
-H "x-message-id: MSG1234" \
-H "x-country_cd: US" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \
```


```JP
-H "x-message-id: MSG1234" \
-H "x-country_cd: JP" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \
```
```GB
-H "x-message-id: MSG1234" \
-H "x-country_cd: GB" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \
```

**Description:** Service for setting up an arrangement using bank account -ACH or debit card details. This service will be used for future dated adhoc payments and auto pays which can be scheduled for a specific day or next payment due date for direct debits/autopays.


**HTTP request**
<span class="hljs-badge-post">POST</span>  https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements


**Request Parameters**

| Name | Location | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| minor_version | query | Service version to invoke. Defaulted to latest version available for the service at the provider. | No | string |
| x-message_id | header | Unique identifier of the request, assigned by the immediate consumer. | Yes | string |
| x-country_cd | header | country code | Yes | string |
| x-tokenization | header | Determines whether SOR should respond with Tokenized/non-Tokenized PII data | Yes | boolean |
| x-amex-target-key | header | environment name for test environments | Yes | string |
| x-message_post_timestamp | header | message post time | Yes | string |
| X-AMEX-API-KEY | header | HMAC API Key | Yes | string |
| Authorization | header | HMAC authorization token. | Yes | string |
| request | body | Request parameters required for setting up an arrangement. | Yes | [arrangement_request](#arrangement_request) |

> Sample Request JSON

```US
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "US",
	"arrangement_currency_code": "USA",
	"payment_program": "AUTOPAY",
	"frequency": "CYCLE_CUT",
	"arrangement_option": "MINIMUM_DUE",
	"offset_day_count": 15,
	"enrollment_id": 123456,
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	}
} 

```


```JP
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "JP",
	"arrangement_currency_code": "JPY",
	"payment_program": "AUTOPAY",
	"frequency": "CYCLE_CUT",
	"arrangement_option": "OPTIONJ",
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	},
	"bank_account_details": {
	    "bank_number":"1234",
	    "branch_number":"123456",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "JP",
		"prefix_name": "æ—¥æœ¬",
		"first_name": "æ°å",
		"last_name": "æ˜­é›„",
		"terms_and_conditions": {
			"terms_and_conditions_version": "DDCL",
			"terms_and_conditions_acceptence_date": "string"
		}
	}
}
```

```GB
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "GB",
	"arrangement_currency_code": "GBP",
	"payment_program": "AUTOPAY",
	"frequency": "CYCLE_CUT",
	"arrangement_option": "FIXED_AMOUNT",
	"arrangement_amount": 100.20,
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	},
	"bank_account_details": {
		"routing_transit_number": "300002",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "GB",
		"prefix_name": "Mr",
		"first_name": "Alex",
		"last_name": "Jones",
		"middle_name": "K",
		"terms_and_conditions": {
			"terms_and_conditions_version": "DDCL",
			"terms_and_conditions_acceptence_date": "string"
		}
	}
}

```

<a name="arrangement_request"></a>**arrangement_request**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| source | string | Unique source enum value given to each of the application consuming the  service by service provider. | Yes |
| last_update_id | string | Last Update id will be stored for audit purposes. If the consuming application is a customer rep channel, CCP ads id is expected and if it is customer interfacing channel , customer's GUID is expected in this field. If either of it is not applicable, any constant text will be honoured. | Yes |
| account_type | string | Customer account type code indicating the type of customer - consumer, corporate, merchant SE, Buyer, Supplier e.t.c. | Yes |
| customer_account_number | string | Unique customer account number. It can be card number, loan number, merchant SE, Buyer , Supplier, Sponsor, RCA based on account_type_cd. | Yes |
| optimistic_transaction_timestamp | dateTime | Optimistic or last read timestamp of the customer account. This field is required if Optimistic_transaction_ind is 'Y'. | No |
| organization_name | string | Organization Name of the customer is required if the customer in request is a corporate or a business. | No |
| prefix_name | string | Individual customer prefix name if the customer is a consumer or an individual | No |
| first_name | string | Individual customer first name if the customer is a consumer or an individual | No |
| last_name | string | Individual customer last name if the customer is a consumer or an individual | No |
| middle_name | string | Individual customer middle name if the customer is a consumer or an individual | No |
| cycle_code | string | Customer Billing cycle id. This is applicable for only corporate card customer account where service provider cannot derive the billing cycle id. | No |
| product_type | string | Product type of the card customer account where AM cannot derive the product type. Currently this field being used only in UK market. | No |
| initiating_country_code | string | FI Account ISO Alpha2 country code | Yes |
| arrangement_currency_code | string | Currency for accepting the arrangement i.e, Allowed currency code (ISO Alpha3) | Yes |
| arrangement_amount | double | Payment/Arrangement amount | No |
| payment_program | string | Service for arrangement | Yes |
| confirmation_text | string | Confirmation Number text where the front end channels will be sending the confirmation nbr to be used for processing the arrangment. | No |
| tracking_id | string | Used by consumer application inorder to trace between applications end to end. This will be used to notify  pub/sub event notifications to downstream. | No |
| sec_code | string | Secondary Entry Class Code applicable only for US ACH Payments. If not sent part of request,it will be derived by application team.Only if consumer of the application wants to control the SEC code they need to pass it. | No |
| clearing_routing_profile | string | Customized profile setup for the consumers who have multiple routing profiles | No |
| frequency | string | This determines how frequently will this arrangement will be active. Based on the service used, this can be one of the values from the below enum list. | Yes |
| week_day_number | integer | Week day number applicable for Weekly autopay arrangements. | No |
| month_day_number | integer | Month Day number applicable for Monthly autopay frequency. | No |
| month_number | integer | Month Number | No |
| offset_day_count | integer | Offset day count which will get to statement generation date and calculate the NPDD ( Next Payment Due Date) | No |
| schedule_date | date | Scheduled date for the arrangement when the monetary transaction will be performed | No |
| arrangement_option | string | Payment Option code indicates the type of payment amount instructed by customer. | No |
| projected_amount | double | This is the amount scheduled to be requested from the CM’s bank account.This is editable between the cycle cut date which assigned it and the date the DD is sent to the bank.  | No |
| amount_percentage | double | If the arrangement_option is “percentage” this will be the percent of the balance being paid in each cycle  | No |
| effective_date | date | Arrangement Effective Date will be the date since when the arrangement date will become active. | No |
| end_date | date | Arrangement End date will confirm the end date of the arrangement depending on service and derived values. | No |
| credit_debit_code | string | Credit Debit indicator denoting the type of transaction | No |
| enrollment_id | integer | Enrollment ID incase where bank details are not provided and previously stored bank account details or bank card need to be used for the payment | No |
| addenda_details | [addenda_details](#addenda_details) | Additional payment-related information pertaining to the entry detail record to which they are attached with for  SecCd 'CTX' or 'CCD' which is passed in NACHA clearing files. | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | Yes |
| bank_account_details | [create_bank_account_details](#create_bank_account_details) | Bank / Debit card details required for adding enrollment. | No |
| bank_card_details | [create_bank_card_details](#create_bank_card_details) | Bank / Debit card details required for adding enrollment. | No |
| optional_request_parameters | [data_element_grp](#data_element_grp)  | Additional parameters passed as part of payload which might have specific project/business related. This needs to be aligned with application team. | No |

> Sample Response JSON

```US
{
  "code": 201,
  "status": "SUCCESS",
  "data": {
    "enrollment": {
      "links": [
        
         {
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				// cancel,modify link is not there since tied to an autopay
        
      ],
      "enrollment_id": 123456,
      "setup_timestamp": ""2017-06-14T04:12:02Z"",
      "effective_date": "2017-04-17",
      "status": "ACTIVE",
      "end_date": "2099-12-31",
      "bank_account_details": {
        "token_id": "string",
        "last4": "5645",
        "bank_name": "bank of america"
      },
    },
    "arrangment_id":"98765",
    "status": "ACTIVE",
    "setup_timestamp": ""2017-06-14T04:12:02Z"",
    "arrangement_currency_code": "USD",
    "next_payment_due_date": "2017-07-10",
   
    "links": [
     {
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/enquiry_results",
				"rel": "self",
				"method": "GET"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
    ]
  }
} 


```


```JP
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				},
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "ACTIVE",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "JPY",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
		]
	}
}
```

```GB
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				// cancel,modify link is not there since tied to an autopay
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "ACTIVE",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "GBP",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
		]
	}
}

```

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 201 | Arrangements | [arrangements_success](#arrangements_success) |
| 400 | Business Exceptions/Validation Failures/Mandatory parameters are missing from request. | [failure](#failure) |
| 401 | Unauthorized/Invalid security header/ApiKey Invalid/MAC signature is invalid/Nonce repeated. | [unauthorized](#unauthorized) |
| 500 | System Exceptions. | [failure](#failure) |
| 504 | External system response timeout. | [failure](#failure) |




<a name="arrangements_success"></a>**arrangements_success**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Code will hold the state of operation performed. It will hold the same code as http request. | Yes |
| status | string | Status will hold the actual result for the operation. For code 200, it will be success while 400 and other scenarios, it will be FAILURE or ERROR. | Yes |
| data | [arrangements_success_data](#arrangements_success_data) | Response block storing the necessary information for Arrangments successful operation. | No |

<a name="arrangements_success_data"></a>**arrangements_success_data**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| enrollment | [enrollment_arrangement](#enrollment_arrangement) | Bank/Debit card associated with the Arrangement. | Yes |
| status | string | Arrangement Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending | No |
| arrangment_id | integer | Arrangement Id generated for the arrangement id. This ID can be used to pull the details of the arrangement | No |
| internal_unique_payment_id | string | Unique Internal Payment Id generated by AM. | No |
| setup_timestamp | dateTime | Setup timestamp in ISO8601 format yyyy-MM-ddTHH:mm:ss+zz:zz. | Yes |
| confirmation_text | string | Confirmation Number text which can be same as what Front end is passing otherwise AM will generate the same. | Yes |
| payment_arngmnt_amount | double | Arrangement amount | Yes |
| arrangement_currency_code | string | Payment Currency | Yes |
| external_unique_payment_id| string | Reference number recived from consumer. | No |
| tracking_id | string | Used by consumer application inorder to trace between applications end to end. This will be sent in payment notification via pub/sub event notifications | No |
| next_payment_due_date | date | Payment planned/scheduled date. | Yes |
| notify_by_date | date | Date by when any edit/cancel requests will be honored before the payment date. | No |
| links | [links_arrangements](#links_arrangements) | Href . | No |

<a name="links_arrangements"></a>**links_arrangements**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | Href | Yes |
| rel | string | Rel | Yes |

## List Arrangements for an Account

> URL

```Any
POST https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/inquiry_results

```
> Header Params

```US
-H "x-message-id: MSG1234" \
-H "x-country_cd: US" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \


```

```JP
-H "x-message-id: MSG1234" \
-H "x-country_cd: JP" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```
```GB
-H "x-message-id: MSG1234" \
-H "x-country_cd: GB" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```


**Description:** Service for inquiring Customer Payments, Active ,Suspended , Cancelled Arrangements and Active , Cancelled and Suspended Bank Enrollments. Modification History related to Arrangements and Bank Enrollments. 



**HTTP request**
<span class="hljs-badge-postiget">POST</span> https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/inquiry_results



**Request Parameters**

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| request | body | Request to Inquire Customer Details. | Yes | [request](#request) |
| minor_version | query | Service version to invoke. Defaulted to latest version available for the service at the provider. | No | string |
| filter | query | filter to apply . <b>sample filter is "filter=status::{active,cancelled}&program::{Autopay}"</b> | No | string |
| x-message_id | header | Unique identifier of the request, assigned by the immediate consumer. | Yes | string |
| x-country_cd | header | country code | Yes | string |
| x-tokenization | header | Determines whether SOR should respond with Tokenized/non-Tokenized PII data | Yes | boolean |
| x-amex-target-key | header | environment name for test environments | Yes | string |
| x-message_post_timestamp | header | message post time | Yes | string |
| X-AMEX-API-KEY | header | HMAC API Key | Yes | string |
| Authorization | header | HMAC authorization token. | Yes | string |

> Sample Request JSON

```US
{
	"source": "MYCA",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "378282246310005",
	"initiating_country_code": "US"
} 

```


```JP
{
	"source": "MYCA",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "378282546310005",
	"initiating_country_code": "JP"
} 
```

```GB
{
	"source": "MYCA",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "378282249310005",
	"initiating_country_code": "GB"
	
}
```
<a name="request"></a>**request** 

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| source | string | Unique source enum value given to each of the application consuming the  service by service provider. | Yes |
| account_type | string | Customer account type code indicating the type of customer - consumer, corporate, merchant SE, Buyer, Supplier e.t.c. | Yes |
| customer_account_number | string | Unique customer account number. It can be card number, loan number, merchant SE, Buyer , Supplier, Sponsor, RCA based on account_type_cd. | Yes |
| initiating_country_code | string | FI Account ISO Alpha2 country code | Yes |
| optional_request_parameters | [data_element_grp](#data_element_grp) | Placeholder for any adhoc feilds to be sent to service provider incase of existing fields does not serve the purpose. Prior alignment with application team is required to use this section. | No |

> Sample Response JSON

```US
{
  "code": 200,
  "status": "SUCCESS",
  "data": {
    "account_type": "CONSUMER_CARD",
    "customer_account_number": "378282246310005",
    "initiating_country_code": "US",
    "arrangements": [
      {
        "enrollment": {
          "links": [
            {
              "href": "https://in.api.dev.aexp.com/remittance/v1/enrollments_mgmt/account/enrollment_details/121432434",
              "rel": "enrollment_details"
            }
          ],
          "enrollment_id": 121432434,
          "account_priority": "009",
          "change_reason": "Customer Request",
          "default_bank_indicator": "YES",
          "mandate_frequency": "RECURRING",
          "mandate_collection_type": "RECURRING",
          "setup_timestamp": "2017-06-16T01:01:24.958-0700",
          "effective_date": "2017-06-16",
          "status": "ACTIVE",
          "suspension_start_date": "2017-09-16",
          "suspension_end_date": "2017-10-16",
          "setup_source": "PS_MYCA",
          "suspension_reason_code": "Customer Request",
          "cancellation_date": "2017-10-16",
          "end_date": "2017-10-16",
          "external_response_description": "success",
          "locked_indicator": [
            true
          ],
          "inuse_indicator": [
            true
          ],
          "last_return_reason_code": "R01",
          "terms_and_conditions": {
            "terms_and_conditions_version": "DDHL",
            "terms_and_conditions_acceptence_date": "2017-01-16"
          },
          "bank_account_details": {
            "routing_transit_number": "122101706",
            "account_number": "12345462",
            "bank_account_type": "CHECKING",
            "owner_type": "INDIVIDUAL",
            "country_code": "US",
            "organization_name": "ABC International",
            "prefix_name": "Sr",
            "first_name": "Andrew",
            "last_name": "Melgar",
            "middle_name": "James",
            "token_id": "jMOAvKBLttdB9hWiMf6c4G5F39RnCXqA",
            "last_return_reason_code": "R01",
            "bank_name": "BMO Harris",
            "last_return_reason_date": "2017-06-16",
            "change_reason": "Customer Request",
            "last_update_details": {
              "last_update_id": "ASA122232443",
              "last_update_timestamp": "2017-06-16T01:01:24.958-0700",
              "update_source": "PS_MYCA"
            },
            "abas_details": [
              {
                "prefix_name": "Mr",
                "first_name": "Andrew",
                "last_name": "Melgar",
                "middle_name": "James",
                "email_address_text": "andy4343@gmail.com"
              }
            ],
            "last_abas_details": {
              "prefix_name": "Mr",
              "first_name": "Andrew",
              "last_name": "Melgar",
              "middle_name": "James",
              "email_address_text": "andy4343@gmail.com"
            }
          },
          "last_abas_details": {
            "prefix_name": "Mr",
            "first_name": "Andrew",
            "last_name": "Melgar",
            "middle_name": "James",
            "email_address_text": "andy4343@gmail.com"
          },
          "last_update_details": {
            "last_update_id": "ASA122232443",
            "last_update_timestamp": "2017-06-16T01:01:24.958-0700",
            "department_id": "D123",
            "update_source": "PS_MYCA"
          }
        },
        "ar_system_date": "2017-06-16",
        "projected_amount": 100,
        "actual_amount": 100,
        "intrimPmtCD": false,
        "last_payment_process_date": "2017-06-16",
        "locked_indicator": "YES",
        "arrangement_id": 76523425,
        "internal_unique_payment_id": "2qTY/d/t55IDdwso1L2ZVA00-63ACA32US0",
        "external_unique_payment_id": "E34564CXZV",
        "payment_label": "EARLY_PAY", 
        "setup_timestamp": "2017-06-16T01:01:24.958-0700",
        "setup_source": "PS_MYCA",
        "confirmation_text": "A1245",
        "arrangement_type": "RECURRING",
        "frequency": "CYCLE_CUT",
        "offset_day_count": 15,
        "schedule_date": "2017-06-16",
        "arrangement_option": "FIXED_AMOUNT",
        "payment_arngmnt_amount": 100,
        "threshold_amount": 5000,
        "arrangement_currency_code": "USD",
        "effective_date": "2017-01-16",
        "end_date": "2099-12-31",
        "suspension_start_date": "2017-08-16",
        "suspension_end_date": "2017-10-16",
        "status": "ACTIVE",
        "cancellation_date": "2017-01-16",
        "suspension_reason": "R01",
        "next_payment_due_date": "2017-07-16",
        "notify_by_date": "2017-07-16",
        "cycle_cut_date": "2017-07-16",
        "payment_type_code": "PT_ONLINE",
        "update_source": "PS_MYCA",
        "terms_and_conditions": {
          "terms_and_conditions_version": "DDHL",
          "terms_and_conditions_acceptence_date": "2017-01-16"
        },
        "change_reason": "Customer Request",
        "return_reason_code": "R01",
        "credit_debit_code": "DEBIT",
        "entry_effective_date": "2017-06-16",
        "company_id": "C1232435",
        "reprocess_payment_indicator": "YES",
        "program_details": {
          "payment_program": "PLUTO_PLAN",
          "locked_indicator": [
            true
          ],
          "direct_debit_indicator": "YES",
          "suspension_reason_code": "R01",
          "suspension_start_date": "2017-06-16",
          "suspension_end_date": "2017-06-16",
          "return_reason_code": 0,
          "effective_date": "2017-06-16",
          "end_date": "2017-06-16",
          "change_reason": "Customer Request",
          "status": "ACTIVE"
        },
        "last_update_details": {
          "last_update_id": "ASA122232443",
          "last_update_timestamp": "2017-06-16T01:01:24.958-0700",
          "update_source": "PS_MYCA"
        }
      }
    ],
    "warning": [
      {
        "code": "RTMAXIMUMPYMTSRCHD",
        "description": "Maximum number of payments has reached"
      }
    ]
   
  }
}

```


```JP
{
  "code": 200,
  "status": "SUCCESS",
  "data": {
    "account_type": "CONSUMER_CARD",
    "customer_account_number": "378282546310005",
    "initiating_country_code": "JP",
    "arrangements": [
      {
        "enrollment": {
          "links": [
            {
              "href": "https://in.api.dev.aexp.com/remittance/v1/enrollments_mgmt/account/enrollment_details/121432434",
              "rel": "enrollment_details"
            }
          ],
          "enrollment_id": 121432434,
          "account_priority": "009",
          "change_reason": "Customer Request",
          "setup_timestamp": "2017-06-16T01:01:24.958-0700",
          "effective_date": "2017-07-05",
          "status": "ACTIVE",
          "setup_source": "PS_JAPA",
          "end_date": "2017-10-16",
          "locked_indicator": [
            false
          ],
          "inuse_indicator": [
            true
          ],
          "terms_and_conditions": {
            "terms_and_conditions_version": "DDHL",
            "terms_and_conditions_acceptence_date": "2017-01-16"
          },
          "bank_account_details": {
            "bank_number": "0005",
            "branch_number": "001",
            "routing_transit_number": "122101706",
            "bank_identifier_code": "OKOYFIHH",
            "account_number": "12345462",
            "check_digit": "09",
            "alternate_bank_name": "Japan Post Bank",
            "alternate_branch_name": "Yokohama Branch",
            "bank_account_type": "CHECKING",
            "owner_type": "INDIVIDUAL",
            "country_code": "JP",
            "prefix_name": "Sr",
            "first_name": "Andrew",
            "last_name": "Melgar",
            "middle_name": "James",
            "token_id": "jMOAvKBLttdB9hWiMf6c4G5F39RnCXqA",
            "bank_name": "Japan Post Bank",
            "bank_risk_indicator": "001",
            "change_reason": "Customer Request",
            "last_update_details": {
              "last_update_id": "ASA122232443",
              "last_update_timestamp": "2017-06-16T01:01:24.958-0700",
              "department_id": "D123",
              "update_source": "PS_JAPA"
            }
          }
        },
        "ar_system_date": "2017-06-16",
        "projected_amount": 100,
        "actual_amount": 100,
        "amount_percentage": 10.5,
        "intrimPmtCD": true,
        "last_payment_process_date": "2017-06-16",
        "locked_indicator": "YES",
        "arrangement_id": 76523425,
        "internal_unique_payment_id": "2qTY/d/t55IDdwso1L2ZVA00-63ACA32US0",
        "external_unique_payment_id": "E34564CXZV",
        "setup_timestamp": "2017-06-16T01:01:24.958-0700",
        "setup_source": "PS_JAPA",
        "confirmation_text": "A1245",
        "arrangement_type": "ADHOC",
        "frequency": "CYCLE_CUT",
        "offset_day_count": 20,
        "schedule_date": "2017-06-16",
        "arrangement_option": "FIXED_AMOUNT",
        "payment_arngmnt_amount": 100.5,
        "arrangement_currency_code": "USD",
        "effective_date": "2017-07-05",
        "end_date": "2017-01-16",
        "status": "ACTIVE",
        "payment_type_code": "PT_ONLINE",
        "update_source": "PS_JAPA",
        "terms_and_conditions": {
          "terms_and_conditions_version": "DDHL",
          "terms_and_conditions_acceptence_date": "2017-01-16"
        },
        "change_reason": "Customer Request",
        "program_details": {
          "payment_program": "AUTOPAY",
          "locked_indicator": [
            true
          ],
          "direct_debit_indicator": "YES",
          "effective_date": "2017-06-16",
          "end_date": "2017-06-16",
          "change_reason": "Customer Request",
          "status": "ACTIVE"
        },
        "last_update_details": {
          "last_update_id": "ASA122232443",
          "last_update_timestamp": "2017-06-16T01:01:24.958-0700",
          "department_id": "D123",
          "update_source": "PS_JAPA"
        }
      }
    ]

  }
}
```

```GB
{
	"code": 200,
	"status": "SUCCESS",
}

```

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Arrangements | [arrangement_details_success](#arrangement_details_success) |
| 400 | Business Exceptions/Validation Failures/Mandatory parameters are missing from request. | [failure](#failure) |
| 401 | Unauthorized/Invalid security header/ApiKey Invalid/MAC signature is invalid/Nonce repeated. | [unauthorized](#unauthorized) |
| 500 | System Exceptions. | [failure](#failure) |
| 504 | External system response timeout. | [failure](#failure) |



<a name="arrangement_details_success"></a>**arrangement_details_success**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Code will hold the state of operation performed. It will hold the same code as http request | Yes |
| status | string | Status will hold the actual result for the operation. For code 200, it will be success while 400 and other scenarios, it will be FAILURE or ERROR. | Yes |
| data | [arrangement_details_data](#arrangement_details_data) | Response block containing the arrangement details | No |

<a name="arrangement_details_data"></a>**arrangement_details_data**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| account_type | string | Customer account type code indicating the type of customer - consumer, corporate, merchant SE, Buyer, Supplier e.t.c. | Yes |
| customer_account_number | string | Unique customer account number. It can be card number, loan number, merchant SE, Buyer , Supplier, Sponsor, RCA based on account_type_cd. | Yes |
| initiating_country_code | string | FI Account ISO Alpha2 country code | Yes |
| arrangements | [arrangements](#arrangements) | Customer account related details will be part of this group. | Yes |
| warning | [warning_details](#warning_details) | Includes warning details (if any applicable). | No |
| optional_request_parameters | [data_element_grp](#data_element_grp) | Placeholder for any adhoc feilds to be sent to service provider incase of existing fields does not serve the purpose. Prior alignment with application team is required to use this section. | No |

<a name="arrangements"></a>**arrangements**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| enrollment | [enrollment](#enrollment) | Bank/Debit card associated with the Arrangement. | Yes |
| ar_system_date | date | The Direct debit date.  This is the date that the DD will post to Globestar and pay down the account.Non-maintainable.   Can zero out the projected DD (within applicable time frame which will then cause this date to be ignored). 
 | No |
| projected_amount | double | The projected amount.  This is the amount scheduled to be requested from the CMs bank account.  It is maintainable between the cycle cut date which assigned it and the date the DD is sent to the bank.
 | No |
| actual_amount | double | The actual DD amount sent to the bank to be collected as well as the amount that will post or has posted in this cycle.  (For example if my Balance is 100 and my scheduled DD is 100 and I do an SE return for 20 then the Actual DD may end up being 80, not 100). Field is non-maintainable (because the DD has happened). 
 | No |
| amount_percentage | float | When the payment method is percentage this will be the percent of the balance being paid each cycle otherwise it will be null/zero
 | No |
| intrimPmtCD | boolean | This will be set to true in UK, and false everywhere else.   There is at present never a need to override the system default.  
 | No |
| last_payment_process_date | date | The last time a DD Occurred on the account | No |
| locked_indicator | string | Determines if the Registration is locked.Occurs when there is active arrangement which is schedule to process in next 24 hrs. | Yes |
| arrangement_id | long | Unique ID generated in AM | Yes |
| internal_unique_payment_id | string | Unique Internal Payment Id generated by AM. | No |
| external_unique_payment_id | string | Payment Id obtained from External Parties | No |
| payment_label | string | Payment label. Applicable for plum cards alone where payment options are presented as payment labels. | No |
| setup_timestamp | dateTime | Setup timestamp in ISO8601 format yyyy-MM-ddTHH:mm:ss+zz:zz. | Yes |
| setup_source | string | Setup source Code which uniquely identifies each of the appication/front end channel | Yes |
| confirmation_text | string | Confirmation Number text | Yes |
| arrangement_type | string | Arrangement Type Id indicates whether its an adhoc arrangement or a recurring instruction. | Yes |
| frequency | string | This determines how frequently will this arrangement will be active. Based on the service used, this can be one of the values from the below enum list. | Yes |
| week_day_number | integer | Week day number applicable for Weekly autopay arrangements. | No |
| month_day_number | integer | Month Day number applicable for Monthly autopay frequency. | No |
| month_number | integer | Month Number | No |
| offset_day_count | integer | Offset day count | No |
| schedule_date | date | Schedule date | No |
| arrangement_option | string | Payment Option code indicates the type of payment amount instructed by customer. | Yes |
| payment_arngmnt_amount | double | Payment/Arrangement amount | Yes |
| threshold_amount | double | Threshold amount | No |
| arrangement_currency_code | string | Arrangement Currency | Yes |
| effective_date | date | Arrangement Effective Date | No |
| end_date | date | Arrangement End date | No |
| suspension_start_date | date | Suspension start date | No |
| suspension_end_date | date | Suspension end date | No |
| status | string | Arrangement Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending | Yes |
| external_response_status_code | string | Response code received from external system. Applicable in markets where payment clearing is real-time | No |
| external_response_reason_text | string | Response description received from external system. Applicable in markets where payment clearing is real-time | No |
| external_response_authorization_code | string | Authorization code received from external system. Applicable in markets where payment clearing is real-time | No |
| cancellation_date | date | Arrangement Cancellation Date | No |
| suspension_reason | integer | Arrangement Suspension reason code | No |
| next_payment_due_date | date | Payment planned/scheduled date. | Yes |
| notify_by_date | date | Date by when any edit/cancel requests will be honored before the payment date. | No |
| cycle_cut_date | date | card account's cycle cut date / statement date of the arrangement effective cycle. | No |
| payment_type_code | string | Payment Type enum based on the type of channel payment was submitted from. | No |
| update_source | string | source enum identifying the channel from where payment was submitted. | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | No |
| change_reason | string | Reason for enrollment. Usually it is 'Customer Request'. | Yes |
| return_reason_code | integer | Return reason code. | No |
| credit_debit_code | string | Credit Debit indicator | No |
| merchant_reference_number | string | Reference number recived from clearing gateway. | No |
| entry_effective_date | date | Effective day of clearing. This field will be used while sending payments to banks. Applicable only for US ACH payments. | No |
| company_id | string | ACH company ID as designated by the clearing bank by remittance program. Applicable for US ACH payments only. | No |
| reprocess_payment_indicator | string | If the payment instruction in the request is a resubmission for originally bank rejected/returned payment. | No |
| program_details | [program_details](#program_details) | Servvice associated with Arrangement. | Yes |
| last_update_details | [last_update_grp](#last_update_grp) |  | Yes |

## Modify an arrangement

> URL

```US
PUT 
https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/{arrangement_id}
```
```JP
PUT 
https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements
```
```GB
PUT 
https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements
```
> Header Params

```US
-H "x-message-id: MSG1234" \
-H "x-country_cd: US" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```


```JP
-H "x-message-id: MSG1234" \
-H "x-country_cd: JP" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```
```GB
-H "x-message-id: MSG1234" \
-H "x-country_cd: GB" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```

**Description:** Service for modifying an arrangement using bank account -ACH or debit card details. This service will be used for modifying the  future dated adhoc payments and auto pays which can be scheduled for a specific day or next payment due date for direct debits/autopays.


**HTTP request**
<span class="hljs-badge-put">PUT</span>  https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/{arrangement_id}
<span class="hljs-badge-put">PUT</span>  https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements

**Request Parameters**

| Name | Location | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| minor_version | query | Service version to invoke. Defaulted to latest version available for the service at the provider. | No | string |
| x-message_id | header | Unique identifier of the request, assigned by the immediate consumer. | Yes | string |
| x-country_cd | header | country code | Yes | string |
| x-tokenization | header | Determines whether SOR should respond with Tokenized/non-Tokenized PII data | Yes | boolean |
| x-amex-target-key | header | environment name for test environments | Yes | string |
| x-message_post_timestamp | header | message post time | Yes | string |
| X-AMEX-API-KEY | header | HMAC API Key | Yes | string |
| Authorization | header | HMAC authorization token. | Yes | string |
| request | body | Request parameters required for setting up an arrangement. | Yes | [arrangement_request](#arrangement_request_update) |

> Sample Request JSON

```US
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "US",
	"arrangement_option": "MINIMUM_DUE",
	"offset_day_count": 20,
	"enrollment_id": 123456,
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	}
} 

```


```JP
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "JP",
	"payment_program": "AUTOPAY",
	"arrangement_option": "OPTIONJ",
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	},
	"bank_account_details": {
	    "bank_number":"1234",
	    "branch_number":"123456",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "JP",
		"prefix_name": "æ—¥æœ¬",
		"first_name": "æ°å",
		"last_name": "æ˜­é›„",
		"terms_and_conditions": {
			"terms_and_conditions_version": "DDCL",
			"terms_and_conditions_acceptence_date": "string"
		}
	}
}
```

```GB
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "GB",
	"payment_program": "AUTOPAY",
	"arrangement_option": "FIXED_AMOUNT",
	"arrangement_amount": 90.20,
	"terms_and_conditions": {
		"terms_and_conditions_version": "DDNL",
		"terms_and_conditions_acceptence_date": "2017-06-14"
	},
	"bank_account_details": {
		"routing_transit_number": "300002",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "GB",
		"prefix_name": "Mr",
		"first_name": "Alex",
		"last_name": "Jones",
		"middle_name": "K",
		"terms_and_conditions": {
			"terms_and_conditions_version": "DDCL",
			"terms_and_conditions_acceptence_date": "string"
		}
	}
}

```

<a name="arrangement_request_update"></a>**arrangement_request**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| source | string | Unique source enum value given to each of the application consuming the  service by service provider. | Yes |
| last_update_id | string | Last Update id will be stored for audit purposes. If the consuming application is a customer rep channel, CCP ads id is expected and if it is customer interfacing channel , customer's GUID is expected in this field. If either of it is not applicable, any constant text will be honoured. | Yes |
| account_type | string | Customer account type code indicating the type of customer - consumer, corporate, merchant SE, Buyer, Supplier e.t.c. | Yes |
| customer_account_number | string | Unique customer account number. It can be card number, loan number, merchant SE, Buyer , Supplier, Sponsor, RCA based on account_type_cd. | Yes |
| optimistic_transaction_timestamp | dateTime | Optimistic or last read timestamp of the customer account. This field is required if Optimistic_transaction_ind is 'Y'. | No |
| organization_name | string | Organization Name of the customer is required if the customer in request is a corporate or a business. | No |
| prefix_name | string | Individual customer prefix name if the customer is a consumer or an individual | No |
| first_name | string | Individual customer first name if the customer is a consumer or an individual | No |
| last_name | string | Individual customer last name if the customer is a consumer or an individual | No |
| middle_name | string | Individual customer middle name if the customer is a consumer or an individual | No |
| cycle_code | string | Customer Billing cycle id. This is applicable for only corporate card customer account where service provider cannot derive the billing cycle id. | No |
| product_type | string | Product type of the card customer account where AM cannot derive the product type. Currently this field being used only in UK market. | No |
| initiating_country_code | string | FI Account ISO Alpha2 country code | Yes |
| arrangement_currency_code | string | Currency for accepting the arrangement i.e, Allowed currency code (ISO Alpha3) | No |
| arrangement_amount | double | Payment/Arrangement amount | No |
| payment_program | string | Service for arrangement | No |
| confirmation_text | string | Confirmation Number text where the front end channels will be sending the confirmation nbr to be used for processing the arrangement. | No |
| tracking_id | string | Used by consumer application inorder to trace between applications end to end. This will be used to notify  pub/sub event notifications to downstream. | No |
| sec_code | string | Secondary Entry Class Code applicable only for US ACH Payments. If not sent part of request,it will be derived by application team.Only if consumer of the application wants to control the SEC code they need to pass it. | No |
| clearing_routing_profile | string | Customized profile setup for the consumers who have multiple routing profiles | No |
| frequency | string | This determines how frequently will this arrangement will be active. Based on the service used, this can be one of the values from the below enum list. | No|
| week_day_number | integer | Week day number applicable for Weekly autopay arrangements. | No |
| month_day_number | integer | Month Day number applicable for Monthly autopay frequency. | No |
| month_number | integer | Month Number | No |
| offset_day_count | integer | Offset day count which will get to statement generation date and calculate the NPDD ( Next Payment Due Date) | No |
| schedule_date | date | Scheduled date for the arrangement when the monetary transaction will be performed | No |
| arrangement_option | string | Payment Option code indicates the type of payment amount instructed by customer. | No |
| projected_amount | double | This is the amount scheduled to be requested from the CM’s bank account.This is editable between the cycle cut date which assigned it and the date the DD is sent to the bank. | No |
| amount_percentage | double | If the arrangement_option is “percentage” this will be the percent of the balance being paid in each cycle  | No |
| effective_date | date | Arrangement Effective Date will be the date since when the arrangement date will become active. | No |
| end_date | date | Arrangement End date will confirm the end date of the arrangement depending on service and derived values. | No |
| credit_debit_code | string | Credit Debit indicator denoting the type of transaction | No |
| enrollment_id | integer | Enrollment ID incase where bank details are not provided and previously stored bank account details or bank card need to be used for the payment | No |
| addenda_details | [addenda_details](#addenda_details) | Additional payment-related information pertaining to the entry detail record to which they are attached with for  SecCd 'CTX' or 'CCD' which is passed in NACHA clearing files. | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | Yes |
| bank_account_details | [create_bank_account_details](#create_bank_account_details) | Bank / Debit card details required for adding enrollment. | No |
| bank_card_details | [create_bank_card_details](#create_bank_card_details) | Bank / Debit card details required for adding enrollment. | No |
| optional_request_parameters | [data_element_grp](#data_element_grp)  | Additional parameters passed as part of payload which might have specific project/business related. This needs to be aligned with application team. | No |

> Sample Response JSON

```US
{
  "code": 200,
  "status": "SUCCESS",
  "data": {
    "enrollment": {
      "links": [
        
         {
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				// cancel,modify link is not there since tied to an autopay
        
      ],
      "enrollment_id": 123456,
      "setup_timestamp": ""2017-06-14T04:12:02Z"",
      "effective_date": "2017-04-17",
      "status": "ACTIVE",
      "end_date": "2099-12-31",
      "bank_account_details": {
        "token_id": "string",
        "last4": "5645",
        "bank_name": "bank of america"
      },
    },
    "arrangment_id":"98765",
    "status": "ACTIVE",
    "setup_timestamp": ""2017-06-14T04:12:02Z"",
    "arrangement_currency_code": "USD",
    "next_payment_due_date": "2017-07-10",
   
    "links": [
     {
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/enquiry_results",
				"rel": "self",
				"method": "GET"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
    ]
  }
} 


```


```JP
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				},
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "ACTIVE",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "JPY",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
		]
	}
}
```

```GB
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				// cancel,modify link is not there since tied to an autopay
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "ACTIVE",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "GBP",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/modification",
				"rel": "modify",
				"method": "PUT"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/cancellation",
				"rel": "cancel",
				"method": "POST"
			}
		]
	}
}

```

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Arrangements | [arrangements_success](#arrangements_success_update) |
| 400 | Business Exceptions/Validation Failures/Mandatory parameters are missing from request. | [failure](#failure) |
| 401 | Unauthorized/Invalid security header/ApiKey Invalid/MAC signature is invalid/Nonce repeated. | [unauthorized](#unauthorized) |
| 500 | System Exceptions. | [failure](#failure) |
| 504 | External system response timeout. | [failure](#failure) |




<a name="arrangements_success_update"></a>**arrangements_success**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Code will hold the state of operation performed. It will hold the same code as http request. | Yes |
| status | string | Status will hold the actual result for the operation. For code 200, it will be success while 400 and other scenarios, it will be FAILURE or ERROR. | Yes |
| data | [arrangements_success_data](#arrangements_success_data_update) | Response block storing the necessary information for Arrangments successful operation. | No |

<a name="arrangements_success_data_update"></a>**arrangements_success_data**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| enrollment | [enrollment_arrangement](#enrollment_arrangement) | Bank/Debit card associated with the Arrangement. | Yes |
| status | string | Arrangement Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending | No |
| arrangment_id | integer | Arrangement Id generated for the arrangement id. This ID can be used to pull the details of the arrangement | No |
| internal_unique_payment_id | string | Unique Internal Payment Id generated by AM. | No |
| setup_timestamp | dateTime | Setup timestamp in ISO8601 format yyyy-MM-ddTHH:mm:ss+zz:zz. | Yes |
| confirmation_text | string | Confirmation Number text which can be same as what Front end is passing otherwise AM will generate the same. | No |
| payment_arngmnt_amount | double | Arrangement amount | Yes |
| arrangement_currency_code | string | Payment Currency | Yes |
| external_unique_payment_id| string | Reference number recived from consumer. | No |
| tracking_id | string | Used by consumer application inorder to trace between applications end to end. This will be sent in payment notification via pub/sub event notifications | No |
| next_payment_due_date | date | Payment planned/scheduled date. | Yes |
| notify_by_date | date | Date by when any edit/cancel requests will be honored before the payment date. | No |
| links | [links_arrangements](#links_arrangements) | Href . | No |

<a name="links_arrangements"></a>**links_arrangements**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | Href | Yes |
| rel | string | Rel | Yes |

## Cancel an arrangement

> URL

```US
POST https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/{arrangement_id}/cancellation
```
```GB
POST 
https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/cancellation
```
```JP
POST 
https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/cancellation
```
> Header Params

```US
-H "x-message-id: MSG1234" \
-H "x-country_cd: US" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```


```JP
-H "x-message-id: MSG1234" \
-H "x-country_cd: JP" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```
```GB
-H "x-message-id: MSG1234" \
-H "x-country_cd: GB" \
-H "x-tokenization: false" \
-H "x-amex-target-key: ze1b" \
-H "x-message_post_timestamp:2017-04-16T10:15:54.442Z" \
-H "X-AMEX-API-KEY: 6tjIKMPDmILtZuEoOkPN2BcGPnX8A5Ksâ€" \
-H "Authorization: pawhKbpZSZgzLaIsdWOfYO6oLJaWCg0z " \

```

**Description:** Service for modifying an arrangement using bank account -ACH or debit card details. This service will be used for modifying the  future dated adhoc payments and auto pays which can be scheduled for a specific day or next payment due date for direct debits/autopays.


**HTTP request**
<span class="hljs-badge-post">POST</span>  https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/{arrangement_id}/cancellation
<span class="hljs-badge-post">POST</span>  https://remittance/v1/arrangements_mgmt/accounts/enrollments/arrangements/cancellation

**Request Parameters**

| Name | Location | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| minor_version | query | Service version to invoke. Defaulted to latest version available for the service at the provider. | No | string |
| x-message_id | header | Unique identifier of the request, assigned by the immediate consumer. | Yes | string |
| x-country_cd | header | country code | Yes | string |
| x-tokenization | header | Determines whether SOR should respond with Tokenized/non-Tokenized PII data | Yes | boolean |
| x-amex-target-key | header | environment name for test environments | Yes | string |
| x-message_post_timestamp | header | message post time | Yes | string |
| X-AMEX-API-KEY | header | HMAC API Key | Yes | string |
| Authorization | header | HMAC authorization token. | Yes | string |
| request | body | Request parameters required for setting up an arrangement. | Yes | [arrangement_request](#arrangement_request_cancel) |

> Sample Request JSON

```US
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "US",
	
} 

```


```JP
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "JP",
	"payment_program": "AUTOPAY",
	"arrangement_option": "NODD",
	"bank_account_details": {
		"routing_transit_number": "300002",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "GB",
		"prefix_name": "æ—¥æœ¬",
		"first_name": "æ°å",
		"last_name": "æ˜­é›„"
		}
	}
```

```GB
{
	"source": "MYCA",
	"last_update_id": "4aa6e5596235b9b4edebcf7111111115",
	"account_type": "CONSUMER_CARD",
	"customer_account_number": "379592294841001",
	"initiating_country_code": "GB",
	"payment_program": "AUTOPAY",
	"arrangement_option": "NODD",
	"bank_account_details": {
		"routing_transit_number": "300002",
		"account_number": "12345678",
		"owner_type": "INDIVIDUAL",
		"country_code": "GB",
		"prefix_name": "Mr",
		"first_name": "Alex",
		"last_name": "Jones",
		"middle_name": "K"
		}
}

```

<a name="arrangement_request_cancel"></a>**arrangement_request**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| source | string | Unique source enum value given to each of the application consuming the  service by service provider. | Yes |
| last_update_id | string | Last Update id will be stored for audit purposes. If the consuming application is a customer rep channel, CCP ads id is expected and if it is customer interfacing channel , customer's GUID is expected in this field. If either of it is not applicable, any constant text will be honoured. | Yes |
| account_type | string | Customer account type code indicating the type of customer - consumer, corporate, merchant SE, Buyer, Supplier e.t.c. | Yes |
| customer_account_number | string | Unique customer account number. It can be card number, loan number, merchant SE, Buyer , Supplier, Sponsor, RCA based on account_type_cd. | Yes |
| optimistic_transaction_timestamp | dateTime | Optimistic or last read timestamp of the customer account. This field is required if Optimistic_transaction_ind is 'Y'. | No |
| initiating_country_code | string | FI Account ISO Alpha2 country code | Yes |
| payment_program | string | Service for arrangement | No |
| arrangement_option | string | Payment Option code indicates the type of payment amount instructed by customer. | No |
| bank_account_details | [create_bank_account_details](#create_bank_account_details) | Bank / Debit card details required for adding enrollment. | No |
| optional_request_parameters | [data_element_grp](#data_element_grp)  | Additional parameters passed as part of payload which might have specific project/business related. This needs to be aligned with application team. | No |

> Sample Response JSON

```US
{
  "code": 200,
  "status": "SUCCESS",
  "data": {
    "enrollment": {
      "links": [
        
         {
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				
        
      ],
      "enrollment_id": 123456,
      "setup_timestamp": ""2017-06-14T04:12:02Z"",
      "effective_date": "2017-04-17",
      "status": "ACTIVE",
      "end_date": "2099-12-31",
      "bank_account_details": {
        "token_id": "string",
        "last4": "5645",
        "bank_name": "bank of america"
      },
    },
    "arrangment_id":"98765",
    "status": "CANCELLED",
    "setup_timestamp": ""2017-06-14T04:12:02Z"",
    "arrangement_currency_code": "USD",
    "next_payment_due_date": "2099-31-12",
   
    "links": [
     {
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/{98765}/enquiry_results",
				"rel": "self",
				"method": "GET"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			}
    ]
  }
} 


```


```JP
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				},
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "CANCELLED",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "JPY",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			}
		]
	}
}
```

```GB
{
	"code": 200,
	"status": "SUCCESS",
	"data": {
		"enrollment": {
			"links": [
				{
					"href": "/remittance/v1/enrollments_mgmt/accounts/enrollments/{123456}",
					"rel": "self",
					"method": "GET"
				}
				// cancel,modify link is not there since tied to an autopay
			],
			"enrollment_id": 123456,
			"setup_timestamp": "2017-06-14T04:12:02Z",
			"effective_date": "2017-04-17",
			"status": "ACTIVE",
			"end_date": "31-12-2099",
			"bank_account_details": {
				"token_id": "string",
				"last4": "5678",
			},
		},
		"status": "CANCELLED",
		"setup_timestamp": "2017-06-14T04:12:02Z",
		"arrangement_currency_code": "GBP",
		"links": [
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results?”filter=program::{Autopay}”",
				"rel": "self",
				"method": "POST"
			},
			{
				"href": "https://HOST/remittance/v1/arrangement_mgmt/accounts/enrollments/arrangements/enquiry_results",
				"rel": "all",
				"method": "POST"
			}
		]
	}
}

```

**Responses**

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Arrangements | [arrangements_success](#arrangements_success_cancel) |
| 400 | Business Exceptions/Validation Failures/Mandatory parameters are missing from request. | [failure](#failure) |
| 401 | Unauthorized/Invalid security header/ApiKey Invalid/MAC signature is invalid/Nonce repeated. | [unauthorized](#unauthorized) |
| 500 | System Exceptions. | [failure](#failure) |
| 504 | External system response timeout. | [failure](#failure) |




<a name="arrangements_success_update"></a>**arrangements_success**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Code will hold the state of operation performed. It will hold the same code as http request. | Yes |
| status | string | Status will hold the actual result for the operation. For code 200, it will be success while 400 and other scenarios, it will be FAILURE or ERROR. | Yes |
| data | [arrangements_success_data](#arrangements_success_data_cancel) | Response block storing the necessary information for Arrangments successful operation. | No |

<a name="arrangements_success_data_cancel"></a>**arrangements_success_data**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| enrollment | [enrollment_arrangement](#enrollment_arrangement) | Bank/Debit card associated with the Arrangement. | Yes |
| status | string | Arrangement Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending | No |
| arrangment_id | integer | Arrangement Id generated for the arrangement id. This ID can be used to pull the details of the arrangement | No |
| internal_unique_payment_id | string | Unique Internal Payment Id generated by AM. | No |
| setup_timestamp | dateTime | Setup timestamp in ISO8601 format yyyy-MM-ddTHH:mm:ss+zz:zz. | Yes |
| confirmation_text | string | Confirmation Number text which can be same as what Front end is passing otherwise AM will generate the same. | No|
| payment_arngmnt_amount | double | Arrangement amount | No|
| arrangement_currency_code | string | Payment Currency | Yes |
| external_unique_payment_id| string | Reference number received from consumer. | No |
| tracking_id | string | Used by consumer application inorder to trace between applications end to end. This will be sent in payment notification via pub/sub event notifications | No |
| next_payment_due_date | date | Payment planned/scheduled date. | Yes |
| notify_by_date | date | Date by when any edit/cancel requests will be honored before the payment date. | No |
| links | [links_arrangements](#links_arrangements) | Href . | No |

<a name="links_arrangements"></a>**links_arrangements**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | Href | Yes |
| rel | string | Rel | Yes |

## Models

<a name="data_element_grp"></a>**data_element_grp**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| name | string | Property name. | Yes |
| value | string | Property value. | Yes |



<a name="addenda_details"></a>**addenda_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| addenda_info | [addenda_information](#addenda_information)  | Addenda Information | Yes |

<a name="addenda_information"></a>**addenda_information**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| addenda_txt | string | Free form text needed for Authentication and Interchange between Banks. Information supplied to enable the matching of an entry with the items that the transfer is intended to settle, eg, commercial invoices in an accounts' receivable system in a structured form | Yes |
| addenda_sequence_nbr | string | Order of free form text to append while sending to bank. | Yes |

<a name="terms_and_conditions"></a>**terms_and_conditions**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| terms_and_conditions_version | string | If available, the version identifier of T & C's the customer has accepted while enrolling. Usually for card customer, its a 4 character version identifier based on card product type. | Yes |
| terms_and_conditions_acceptence_date | date | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | Yes |

<a name="create_bank_account_details"></a>**create_bank_account_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| save_bank_indicator | boolean | Boolean value Indicating whether to save bank for future use. | No |
| bank_number | string | Identification number of the bank. Payables uses this information to identify the bank in payment formats that use electronic payment methods. The combination of Bank Number, Branch Number, and Country must be unique. | No |
| branch_number | string | Identification number of the branch. Payables uses this information to identify the bank in payment formats that use electronic payment methods. The combination of Bank Number, Branch Number, and Country must be unique. | No |
| routing_transit_number | string | Routing Transit number for US/Sort Code for International/Zengin Code for Japan. The Zengin code for a bank company comprises 4 digits, with 3 more digits added to identify the branch  . | No |
| bank_identifier_code | string | BIC Code for International markets . | No |
| account_number | string | The bank account identification number. . | No |
| iban_number | string | The IBAN is an international standard that uniquely identifies the account number of a bank's customer. It is used in euro-zone countries to help ensure error-free cross-border payments. The IBAN is validated upon entry. If you provide the IBAN on your supplier's bank account, then it is recommended that you also provide the BIC for that supplier's bank branch. | No |
| clabe | string | The CLABE(Clave Bancaria Estandarizada, Spanish for "standardized banking cipher") is a banking standard for the numbering of bank accounts in Mexico. This standard is a requirement for the sending and receiving of domestic inter-bank electronic funds transfer. | No |
| check_digit | string | The value used to validate the authenticity of your bank account number according to country specific bank account validation requirements. This value is provided by your financial institution. | No |
| alternate_bank_name | string | You can enter an alternate name for your bank. This is particularly useful if you do business in Japan, which allows you to enter both Kanji and Kana values for your bank name. | No |
| alternate_branch_name | string | You can enter an alternate name for your bank branch. This is particularly useful if you do business in Japan, which allows you to enter both Kanji and Kana values for your bank branch name. | No |
| bank_account_type | string | Bank account type. The seeded values are SAVING, CHECKING and OTHER. For example, you could add Controlled Disbursement for your internal bank account. Checking would be used for a supplier or customer bank account. | Yes |
| owner_type | string | Indicates account owner type - Individual, Small business or Corporate | Yes |
| country_code | string | FI Account ISO Alpha2 country code | Yes |
| organization_name | string | Organization name as appears on bank account if it is owned by a corporate or a business. | No |
| prefix_name | string | Customer prefix name as appears on bank account. | No |
| first_name | string | Customer first name as appears on bank account. | No |
| last_name | string | Customer last name as appears on the bank account. | No |
| middle_name | string | Customer middle name as it appears on the bank account. | No |
| token_id | string | Token complaint with PCI-DSS. | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | No |

<a name="create_bank_card_details"></a>**create_bank_card_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| enrollment_id | integer | Enrollment ID incase where bank details are not provided. | No |
| save_bank_card_indicator | boolean | Boolean value Indicating whether to save bank for future use. | No |
| card_number | string | Bank Account Number(for Bank enrollments) and Debit card number (for debit            card enrollments) | Yes |
| owner_type | string | Indicates account owner type - Individual, Small business or Corporate | Yes |
| embossed_name | string | Name embossed on debit card for debit card enrollment. | Yes |
| expiry_date | string | Debit card expiry date in mm/yy format | Yes |
| start_date | string | Debit card start date in mm/yy format | No |
| issuer_number | string | Debit card issuer number | Yes |
| card_type_text | string | Debit card type | No |
| card_scheme_type | string | Debit card network type - VISA/MASTER CARD/SOLO e.t.c | No |
| address_line1_text | string | Street Address | No |
| adress_city_name | string | City Name | No |
| address_region_area_code | string | State | No |
| address_country_code | string | country code | Yes |
| address_postal_code | string | zip/postal code | Yes |
| token_id | string | Token complaint with PCI-DSS. | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | No |


<a name="program_details"></a>**program_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| payment_program | string | Unique Id generated by EMM for a registration during setup. | Yes |
| locked_indicator |  string  | Indicates that enrollment is Locked and cannot be updated/cancelled.
 | Yes |
| direct_debit_indicator | string | Direct Debit indicator used primarily for Corporate card programs. | No |
| suspension_reason_code | integer | Reason code for suspending the registration. | No |
| suspension_start_date | date | Date when suspension is active | No |
| suspension_end_date | date | Date when suspension ends | No |
| return_reason_code | integer | Return reason code. | No |
| effective_date | date | Effective date of registration | Yes |
| end_date | date | End date of registration | Yes |
| change_reason | string | Change reason code | Yes |
| status | string | Status code | Yes |

<a name="enrollment"></a>**enrollment**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| links | [links](#links)  | Href . | No |
| enrollment_id | long | Unique enrollment id assigned by EMM. | Yes |
| account_priority | string | Bank or debit card enrollment priority code incase multiple enrollment for a customer account are allowed in the respective market. '1' is the high priority or default bank. | No |
| change_reason | string | Reason for enrollment. Generally its based on request from Customer. | Yes |
| default_bank_indicator | string | Indicator to make bank / debit card enrollment is a default enrollment. | Yes |
| security_code_validation_required | string | This field is applicable for Debit card enrollments if Security code / CVV2 code needs to be validated for its length. Currently its applicable only in UK market. | No |
| national_id_type | string | National Identifier type. In certain markets its required to share customer's national identifier to complete the mandate process. Any national id or passport will be considered under this. | No |
| national_id | string | National Identifier number of the customer. | No |
| mandate_frequency | string | Payment Frequencies(adhoc/recurring) allowed for the respective enrollment mandate. | No |
| mandate_collection_type | string | Mandate collection type. Cuurently used in IN/HK markets. | No |
| setup_timestamp | dateTime | setup time stamp in market local timezone at the time enrollment. | Yes |
| effective_date | date | effective date of the enrollment | Yes |
| status | string | Enrollment Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending; 5- Deffered | Yes |
| suspension_start_date | date | Suspension start date of the enrollment | No |
| suspension_end_date | date | Date when suspension ends | No |
| setup_source | integer | Setup source Code which uniquely identifies each of the appication/front end. | Yes |
| suspension_reason_code | string | suspension reason code captured during the suspension if the respective enrollment is in suspended status. | No |
| cancellation_date | date | Enrollment Cancelled Date. | No |
| end_date | date | Enrollment end date. | Yes |
| external_response_code | string | External system reason code for Enrollment setup. | No |
| external_response_description | string | External system reason description for Enrollment setup.. | No |
| card_security_validation_status | string | Debit card security code validation status. | No |
| locked_indicator |  string  | Indicates that enrollment is Locked and cannot be updated/cancelled.
 | No |
| inuse_indicator |  string  | Indicates that enrollment is Locked and cannot be updated/cancelled.
 | No |
| return_strike_count | integer | return count for the current bank. | No |
| last_return_reason_code | string | return reason code | No |
| terms_and_conditions | [terms_and_conditions](#terms_and_conditions) | Date on which customer has accepted T & C for adding the bank/ debit card enrollment. | Yes |
| bank_account_details | [bank_account_details](#bank_account_details) | Bank / Debit card details required for adding enrollment. | No |
| bank_card_details | [bank_card_details](#bank_card_details) | Bank / Debit card details required for adding enrollment. | No |
| last_abas_details | [abas_details](#abas_details) | Corporate Authorized ABOs for bank enrollments. | No |
| last_update_details | [last_update_grp](#last_update_grp) | Last update details | Yes |

<a name="links"></a>**links**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| href | string | Href | Yes |
| rel | string | Rel | Yes |

<a name="bank_account_details"></a>**bank_account_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| bank_number | string | Identification number of the bank. Payables uses this information to identify the bank in payment formats that use electronic payment methods. The combination of Bank Number, Branch Number, and Country must be unique. | No |
| branch_number | string | Identification number of the branch. Payables uses this information to identify the bank in payment formats that use electronic payment methods. The combination of Bank Number, Branch Number, and Country must be unique. | No |
| routing_transit_number | string | Routing Transit number for US/Sort Code for International/Zengin Code for Japan. The Zengin code for a bank company comprises 4 digits, with 3 more digits added to identify the branch  . | No |
| bank_identifier_code | string | BIC Code for International markets . | No |
| account_number | string | The bank account identification number. . | No |
| iban_number | string | The IBAN is an international standard that uniquely identifies the account number of a bank's customer. It is used in euro-zone countries to help ensure error-free cross-border payments. The IBAN is validated upon entry. If you provide the IBAN on your supplier's bank account, then it is recommended that you also provide the BIC for that supplier's bank branch. | No |
| clabe | string | The CLABE(Clave Bancaria Estandarizada, Spanish for "standardized banking cipher") is a banking standard for the numbering of bank accounts in Mexico. This standard is a requirement for the sending and receiving of domestic inter-bank electronic funds transfer. | No |
| check_digit | string | The value used to validate the authenticity of your bank account number according to country specific bank account validation requirements. This value is provided by your financial institution. | No |
| alternate_bank_name | string | You can enter an alternate name for your bank. This is particularly useful if you do business in Japan, which allows you to enter both Kanji and Kana values for your bank name. | No |
| alternate_branch_name | string | You can enter an alternate name for your bank branch. This is particularly useful if you do business in Japan, which allows you to enter both Kanji and Kana values for your bank branch name. | No |
| bank_account_type | string | Bank account type. The seeded values are SAVING, CHECKING and OTHER. For example, you could add Controlled Disbursement for your internal bank account. Checking would be used for a supplier or customer bank account. | Yes |
| owner_type | string | Indicates account owner type - Individual, Small business or Corporate | Yes |
| country_code | string | FI Account ISO Alpha2 country code | Yes |
| organization_name | string | Organization name as appears on bank account if it is owned by a corporate or a business. | No |
| prefix_name | string | Customer prefix name as appears on bank account. | No |
| first_name | string | Customer first name as appears on bank account. | No |
| last_name | string | Customer last name as appears on the bank account. | No |
| middle_name | string | Customer middle name as it appears on the bank account. | No |
| token_id | string | Token complaint with PCI-DSS. | No |
| last_return_reason_code | string | return reason code | No |
| bank_name | string | FI Name. | Yes |
| last_return_reason_date | date | Return date. | No |
| bank_risk_indicator | string | Bank Risk Indicator. | Yes |
| change_reason | string | Reason for enrollment. Usually it is 'Customer Request'. | Yes |
| last_update_details | [last_update_grp](#last_update_grp) | Last update details | Yes |
| abas_details | [abas_details](#abas_details)  | Corporate Authorized ABOs for bank enrollments. | No |
| last_abas_details | [abas_details](#abas_details) | Corporate Authorized ABOs for bank enrollments. | No |

<a name="bank_card_details"></a>**bank_card_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| card_number | string | Bank Account Number(for Bank enrollments) and Debit card number (for debit            card enrollments) | Yes |
| owner_type | string | Indicates account owner type - Individual, Small business or Corporate | Yes |
| bank_account_type | string | Bank account type. The seeded values are SAVING, CHECKING and OTHER. For example, you could add Controlled Disbursement for your internal bank account. Checking would be used for a supplier or customer bank account. | Yes |
| embossed_name | string | Name embossed on debit card for debit card enrollment. | No |
| expiry_date | string | Debit card expiry date in mm/yy format | No |
| start_date | string | Debit card start date in mm/yy format | No |
| issuer_number | string | Debit card issuer number | No |
| card_type_text | string | Debit card type | No |
| card_scheme_type | string | Debit card network type - VISA/MASTER CARD/SOLO e.t.c | Yes |
| address_line1_text | string | Street Address | No |
| adress_city_name | string | City Name | No |
| address_region_area_code | string | State | No |
| address_country_code | string | country code | Yes |
| address_postal_code | string | zip/postal code | No |
| last_return_reason_code | string | return reason code | No |
| token_id | string | Token complaint with PCI-DSS. | No |
| last_return_reason_date | date | Return date. | No |
| card_expire_indicator | string | Debit Card expired Indicator. | No |
| bank_risk_indicator | string | Bank Risk Indicator. | Yes |
| change_reason | string | Reason for enrollment. Usually it is 'Customer Request'. | Yes |
| address_validation_status | integer | Address validation | No |
| last_update_details | [last_update_grp](#last_update_grp) | Last update details | Yes |
| abas_details |  [abas_details](#abas_details)  | Corporate Authorized ABOs for bank enrollments. | No |
| last_abas_details | [abas_details](#abas_details) | Corporate Authorized ABOs for bank enrollments. | No |

<a name="enrollment_arrangement"></a>**enrollment_arrangement**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| links |  [links](#links)  | Href . | No |
| enrollment_id | integer | Unique enrollment id assigned by EMM. | Yes |
| setup_timestamp | dateTime | setup time stamp in market local timezone at the time enrollment. This will follow ISO8601 format. | Yes |
| effective_date | date | effective date of the enrollment | Yes |
| status | string | Enrollment Status code. 1 - Active; 2- Suspended; 3- Cancelled; 4- Pending | Yes |
| end_date | date | Enrollment end date. | Yes |
| bank_account_details | [bank_account_details2](#bank_account_details2) | Bank / Debit card details required for adding enrollment. | No |
| bank_card_details | [bank_card_details2](#bank_card_details2) | Bank / Debit card details required for adding enrollment. | No |

<a name="bank_account_details2"></a>**bank_account_details2**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| token_id | string | Token complaint with PCI-DSS. | No |
| last4 | string | The bank account identification number. . | Yes |
| bank_name | string | FI Name. | No |

<a name="bank_card_details2"></a>**bank_card_details2**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| token_id | string | Token complaint with PCI-DSS. | No |
| last4 | string | Bank Account Number(for Bank enrollments) and Debit card number (for debit card enrollments) | Yes |
| card_type_text | string | Debit card type | No |
| card_scheme_type | string | Debit card network type - VISA/MASTER CARD/SOLO e.t.c | No |

<a name="last_update_grp"></a>**last_update_grp**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| last_update_id | string | Last Update Id. | Yes |
| last_update_timestamp | dateTime | Last update Timestamp in ISO8601 format yyyy-MM-ddTHH:mm:ss+zz:zz. | Yes |
| department_id | string | Department Id used to update FI. | No |
| update_source | string | Update Source Cd | Yes |

<a name="abas_details"></a>**abas_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| prefix_name | string | ABO's Prefix name. | No |
| first_name | string | ABO's First name. | Yes |
| last_name | string | ABO's Last name. | Yes |
| middle_name | string | ABO's middle name. | No |
| email_address_text | string | ABO's email id. | No |

<a name="warning_details"></a>**warning_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | string | Warning code | Yes |
| description | string | Warning description | Yes |

<a name="failure"></a>**failure**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Code will hold the state of operation performed. It will hold the same code as http request. | Yes |
| status | string | Status will hold the actual result for the operation. For code 200, it will be success while 400 and other scenarios, it will be FAILURE or ERROR. | Yes |
| message | string | Description of error | Yes |
| data | [failure_data](#failure_data) | TODO | Yes |

<a name="failure_data"></a>**failure_data**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| customer_account_number | string | customer account number. | Yes |
| error_details |  [error_details](#error_details)  | Error details. | Yes |

<a name="error_details"></a>**error_details**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error_code | string | AM error code representing the reason of failure. | Yes |
| error_text | string | Descriptive text of the failure reason. | Yes |
| error_data_list |  [error_data_list](#error_data_list)  | Additional details corresponding to the error code. | No |

<a name="error_data_list"></a>**error_data_list**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error_data_name | string | Error data parameter name | Yes |
| error_data_text | string | Error data parameter text | Yes |

<a name="unauthorized"></a>**unauthorized**  

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| error_type | string | error code representing the reason of failure. | Yes |
| error_code | string | Descriptive text of the failure reason. | Yes |
| error_description | string | Descriptive text of the failure reason. | Yes |




