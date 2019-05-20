Cash is the most straightforward payment method to integrate.

!!! Tip

    Visit [Wirecard](https://www.wirecard.com/payment-base/pos) website to find out all benefits of Wirecard ePOS solution.

!!! Note
    
    Sale requests are serviced at https://switch.wirecard.com/mswitch-server/v1/sales URL.

## Purchase Operation

In context of Wirecard ePOS, every payment transaction (alias payment) is part of a _Sale_. In order to process cash payment, call Wirecard ePOS with _Sale-PURCHASE_ request defined below:

### Request
    
    {
        "multitender": "true",
        "operation" : "PURCHASE",
        "externalId": "123456789",
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

- **"multitender"** - boolean flag
    - "TRUE" - required; compliant with newest Sale Model, which is described in this integration guide
    - "FALSE" - deprecated; old Sale Model is not addressed in this integration guide
- **"operation"** - defines type of Sale request; "PURCHASE" operation creates new Sale-Purchase record
- **_"note"_** - _optional_ - note is forwarded to payment gateway
- **_"externalId"_** - _optional_ - meant to be used for integrator tracking purpose; it is forwarded to payment gateway
- **"totalAmount"** - defines amount of Sale-Purchase 
- **"currencyCode"** - defines currency, based on [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) standard
- **"payments"** - payment-specific information; one payment transaction per request is supported
    - **"paymentMethod"** - defines payment method
    - **"transactionType"** - defines type of this transaction; "PURCHASE" transaction type moves funds from end-consumer to merchant
    - **"amount"** - defines transaction amount

!!! Note

    In context of Wirecard ePOS, term **Purchase** is used for both:
    
    - type of Sale - defined more specifically as _Sale-Purchase_
    - transaction type - e.g. cash _purchase_ transaction, card _purchase_ transaction, etc.

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
    
- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1000" means operation is successful
    - **"result"** - "SUCCESS" means operation is successful
- **"id"** - Sale-Purchase identifier assigned by Wirecard ePOS system
- **"externalCashierId"** - relevant for [Advanced Integration](advanced_overview.md); otherwise null
- **"payments"** - specific information for every payment method
    - **"paymentMethod"** - echoed from request
    - **"transactionType"** - echoed from request
    - **"id"** - identifier of purchase transaction assigned by Wirecard ePOS system
    - **"timeStamp"** - date-time when transaction was processed by payment gateway
    - **"statuses"**
        - **"result"** - "SUCCESS" means transaction is successful
        - **"code"** - code "1000" means transaction is successful
        - **"message"** - message provided by payment gateway
- **"externalId"** - echoed from request
- **"merchantReceiptId"** - unique identifier per merchant; it is incremented with every Sale-Purchase and Sale-Return; advised to be printed on receipt as barcode
- **"multitender"** - echoed from request

!!! Important
    
    After successful PURCHASE operation, [GET a Sale call](#get-a-sale-call) is advised, as it provides complete Sale information.

## Reverse & Cancel Operation

_REVERSE_ operation is typically used in case _Sale-Purchase_ was created accidentally. _REVERSE_ operation serves for reversing particular _purchase_ transaction.

_CANCEL_ operation is used to change state of Sale-Purchase to CANCELED. _CANCEL_ operation can be sent only as long as the purchase transaction is reversed. 

In order to reverse cash purchase transaction, call Wirecard ePOS with _Sale-REVERSE_ request defined below:

### Reverse Request

    {
        "operation": "REVERSE",
        "originalSaleId": "bdb7dd5566f043ab9b91108863a6e833",
        "payments": [
            { 
                "paymentMethod": "CASH",
                "transactionType": "REVERSAL",
                "originalTransactionId" : "2d08be0814f04cc1a2b2b9b5cd1273e2"
            }
        ]
    }

- **"operation"** - defines type of Sale request
- **"originalSaleId"** - identifier of original Sale-Purchase
- **"payments"** - payment-specific information; one payment transaction per request is supported
    - **"paymentMethod"** - defines payment method; it must be same as original payment transaction
    - **"transactionType"** - defines type of this transaction; REVERSE operation must include REVERSAL transaction type
    - **"originalTransactionId"** - identifier of original purchase transaction

### Reverse Response

    {
        "operation": "REVERSE",
        "timeStamp": "2019-04-11T06:49:51.541Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "bdb7dd5566f043ab9b91108863a6e833",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "CASH",
                "transactionType": "REVERSAL",
                "id": "6f5789c304594fe8a796d5b2bdaebbf0",
                "timeStamp": "2019-04-11T06:49:51.532Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ]
            }
        ]
    }

- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1000" means operation is successful
    - **"result"** - "SUCCESS" means operation is successful
- **"id"** - echoed from request; Sale-Purchase identifier
- **"externalCashierId"** - relevant for [Advanced Integration](advanced_overview.md); otherwise null
- **"payments"** - specific information for every payment method
    - **"paymentMethod"** - echoed from request
    - **"transactionType"** - echoed from request
    - **"id"** - identifier of reversal transaction
    - **"timeStamp"** - date-time when reversal transaction was processed by payment gateway
    - **"statuses"**
        - **"result"** - "SUCCESS" means transaction is successful
        - **"code"** - code "1000" means transaction is successful
        - **"message"** - message provided by payment gateway
        
In order to explicitly change state of Sale-Purchase to CANCELED, call Wirecard ePOS with _Sale-CANCEL_ request defined below:

### Cancel Request

    {
        "operation": "CANCEL",
        "originalSaleId": "bdb7dd5566f043ab9b91108863a6e833"
    }
    
- **"operation"** - defines type of Sale request
- **"originalSaleId"** - identifier of original Sale-Purchase

### Cancel Response

    {
        "operation": "CANCEL",
        "timeStamp": "2019-04-11T13:30:05.187Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "bdb7dd5566f043ab9b91108863a6e833",
        "externalCashierId": null
    }
    
- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1000" means operation is successful
    - **"result"** - "SUCCESS" means operation is successful
- **"id"** - echoed from request; Sale-Purchase identifier
- **"externalCashierId"** - relevant for [Advanced Integration](advanced_overview.md); otherwise null

## Return Operation

_RETURN_ operation is used in case end-consumer returns merchandise and asks for a refund. Wirecard ePOS support partial as well as full returns.

In order to refund cash purchase transaction, call Wirecard ePOS with _Sale-RETURN_ request defined below:

### Request

    {
        "operation" : "RETURN",
        "note" : "My First Return",
        "externalId" : "20190411001",
        "totalAmount" : 10,
        "currencyCode" : "EUR",
        "originalSaleId" : "344009e1f53a4dd0af9751f0b7d7d99d",
        "payments" : [
            {
                "paymentMethod" : "CASH",
                "transactionType" : "REFUND",
                "amount" : 10
            }
        ]
    }

- **"operation"** - defines type of Sale request
- **_"note"_** - _optional_ - note is forwarded to payment gateway
- **_"externalId"_** - _optional_ - meant to be used for integrator tracking purpose; it is forwarded to payment gateway
- **"totalAmount"** - defines amount to be refunded; it can be equal (full return) or less (partial return) than totalAmount in original Sale-Purchase
- **"currencyCode"** - must be same as for original Sale-Purchase
- **"originalSaleId"** - identifier of original Sale-Purchase
- **"payments"** - payment-specific information; one payment transaction per request is supported
    - **"paymentMethod"** - defines payment method
    - **"transactionType"** - defines type of this transaction; must be "REFUND" when payment method is CASH
    - **"amount"** - defines amount to be refunded

### Response

    {
        "operation": "RETURN",
        "timeStamp": "2019-04-11T09:55:15.594Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "5c0e6ef0da784b8c940b488ef6f0cb8b",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "CASH",
                "transactionType": "REFUND",
                "id": "2fec6d42713a4703a4422b1359c2b588",
                "timeStamp": "2019-04-11T09:55:15.575Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ]
            }
        ],
        "externalId": "20190411001",
        "merchantReceiptId": 467
    }

- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1000" means operation is successful
    - **"result"** - "SUCCESS" means operation is successful
- **"id"** - Sale-Return identifier assigned by Wirecard ePOS
- **"externalCashierId"** - relevant for [Advanced Integration](advanced_overview.md); otherwise null
- **"payments"** - specific information for every payment method
    - **"paymentMethod"** - echoed from request
    - **"transactionType"** - echoed from request
    - **"id"** - identifier of refund transaction assigned by Wirecard ePOS system
    - **"timeStamp"** - date-time when transaction was processed by payment gateway
    - **"statuses"**
        - **"result"** - "SUCCESS" means transaction is successful
        - **"code"** - code "1000" means transaction is successful
        - **"message"** - message provided by payment gateway
- **"externalId"** - echoed from request
- **"merchantReceiptId"** - unique identifier per merchant; it is incremented with every Sale-Purchase and Sale-Return; advised to be printed on receipt as barcode

!!! Tip
    See also complete list of Wirecard ePOS Sale [request & response examples](https://switch-test.wirecard.com/mswitch-server/doc/api-doc-sale-examples.html).
    
## GET a Sale Call

You can see below an example of GET a Sale call with excluded _merchant_ and _user_ fields which are going to be described in [Merchant Management](merchant-management.md) and [User Management](user.md) respectively.
    
    GET https://switch-test.wirecard.com/mswitch-server/v1/sales/19267cf3a3cb4e2d8131917b5c092a0d?excludeField=merchant&excludeField=user
    
    {
          "id": "19267cf3a3cb4e2d8131917b5c092a0d",
          "type": "PURCHASE",
          "status": "COMPLETED",
          "totalAmount": 10,
          "note": "My First Sale",
          "externalId": null,
          "externalCashierId": null,
          "customerId": null,
          "initialized": "2019-04-11T13:36:11.521Z",
          "shop": null,
          "currency": {
                "number": 978,
                "code": "EUR",
                "name": "Euro",
                "minorUnit": 2
          },
          "unitPricesIncludeTax": null,
          "items": [
          ],
          "transactions": [
                {
                      "type": "CASH_PURCHASE",
                      "id": "7a8f701dd40743e0ad942ae32cd0e9d8",
                      "status": "COMPLETED",
                      "amount": 10,
                      "lastUpdated": "2019-04-11T13:36:11.597Z",
                      "initialized": "2019-04-11T13:36:11.521Z",
                      "message": null
                }
          ],
          "location": null,
          "clientInfo": null,
          "merchantReceiptId": 245,
          "cancelledBy": null,
          "shiftId": null,
          "cashRegisterId": null,
          "emailForReceipt": null,
          "emailForReceiptProvided": false,
          "multitender": true
    }
