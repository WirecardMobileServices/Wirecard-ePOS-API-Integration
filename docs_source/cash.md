Cash is the simplest payment method to integrate. Cash is one-step payment method what means that only one request to Wirecard ePOS API is needed.

!!! Note
    
    Sale requests are serviced at https://switch.wirecard.com/mswitch-server/v1/sales URL.

### Request
    
    {
        "multitender": "true",
        "operation" : "PURCHASE",
        "note": "My First Sale",
        "externalId": "123456789",
        "totalAmount" : 10.0,
        "currencyCode" : "EUR",
        "payments" : [
            {
                "paymentMethod" : "CASH",
                "transactionType" : "PURCHASE",
                "amount" : 10.0
            }
        ]
    }

Every element from request is described below:

- "multitender" - boolean flag
    - set "TRUE" in order to be compliant with newest Sale Model
    - setting "FALSE" or omitting this element is possible, however it is not advised as the previous Sale model is deprecated
- "operation" - "PURCHASE" operation creates new Sale-Purchase record
- "note" - optional - it is forwarded to payment gateway
- "externalId" - optional - meant to be used for integrator tracking purpose; it is forwarded to payment gateway
- "totalAmount" - amount of funds end-consumer has to pay
- "currencyCode" - based on ISO 4217 standard
- "payments" - even though it is an array, only one payment per request is supported at the moment
    - "paymentMethod" - "CASH" stands for cash payment method
    - "transactionType" - "PURCHASE" transaction type moves funds from end-consumer to merchant
    - "amount" - payment transaction amount

### Response

    {
        "operation": "PURCHASE",
        "timeStamp": "2019-04-10T09:41:39.597Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "bdb7dd5566f043ab9b91108863a6e833",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "CASH",
                "transactionType": "PURCHASE",
                "id": "2d08be0814f04cc1a2b2b9b5cd1273e2",
                "timeStamp": "2019-04-10T09:41:39.554Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ]
            }
        ],
        "externalId": null,
        "merchantReceiptId": 457,
        "multitender": true
    }
    
Every element from response is described below:

- "operation" - echoed from request
- "timeStamp" - date-time when response was constructed
- "status"
    - "code" - code "1000" means operation is successful (taken from _payments.statuses.code_)
    - "result" - "SUCCESS" means operation is successful (taken from _payments.statuses.result_)
- "id" - Sale-Purchase identifier assigned by Wirecard ePOS system
- "externalCashierId" - relevant for [Advanced Integration](advanced_overview.md)
- "payments" - specific for every payment method
    - "paymentMethod" - echoed from request
    - "transactionType" - echoed from request
    - "id" - identifier of payment transaction assigned by Wirecard ePOS system
    - "timeStamp" - date-time when transaction was processed by payment gateway
    - "statuses"
        - "result" - "SUCCESS" means transaction is successful
        - "code" - code "1000" means transaction is successful
        - "message" - message provided by payment gateway
- "externalId" - echoed from request
- "merchantReceiptId" - identifier unique only for merchant; it is incremented with every Purchase and Return; advised to be printed on receipt as barcode
- "multitender" - echoed from request
    
!!! Tip
    See also complete list of Wirecard ePOS Sale [request & response examples](https://switch-test.wirecard.com/mswitch-server/doc/api-doc-sale-examples.html).