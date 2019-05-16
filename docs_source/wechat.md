WeChat is one-step payment method in case end-consumer is not required to authorize payment on his device.

In case end-consumer has to authorize the payment with password or other equivalent (pin code, fingerprint, etc.) then WeChat payment has to be confirmed by follow-up CONFIRM request.

!!! Tip
    
    For more details regarding WeChat Pay, visit [Wirecard China Payment](https://www.wirecard.com/chinapayment/en/) website.

!!! Note
    
    Sale requests are serviced at https://switch.wirecard.com/mswitch-server/v1/sales URL.
    
## Purchase Operation

In context of Wirecard ePOS, every payment transaction is part of a _Sale_. In order to process WeChat payment, call Wirecard ePOS API with _Sale-PURCHASE_ request defined below:

### Request

    {
        "multitender": "true",
        "operation" : "PURCHASE",
        "totalAmount" : 10,
        "currencyCode" : "EUR",
        "payments" : [
            {
                "paymentMethod" : "WECHAT",
                "transactionType" : "PURCHASE",
                "amount" : 10,
                "consumerId" : "15050011719660761"
            }
        ]
    }
    
- **"multitender"** - boolean flag
    - "TRUE" - required; compliant with newest Sale Model, which is described in this integration guide
    - "FALSE" - deprecated; old Sale Model is not addressed in this integration guide
- **"operation"** - defines type of Sale request; "PURCHASE" operation creates new Sale-Purchase record
- **_"externalId"_** - _optional_ - meant to be used for integrator tracking purpose; it is forwarded to payment gateway
- **"totalAmount"** - defines amount of Sale-Purchase 
- **"currencyCode"** - defines currency, based on [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) standard
- **"payments"** - payment-specific information; one payment transaction per one request is supported
    - **"paymentMethod"** - defines payment method
    - **"transactionType"** - defines type of this transaction; "PURCHASE" transaction type moves funds from end-consumer to merchant
    - **"amount"** - defines transaction amount
    - **"consumerId"** - value of scanned barcode (QR code)

!!! Note

    In context of Wirecard ePOS, term **Purchase** is used for both:
    
    - type of Sale - defined more specifically as _Sale-Purchase_
    - transaction type - e.g. alipay _purchase_ transaction, cash _purchase_ transaction, etc.

### Response indicating 1-step WeChat payment

In order to identify whether the follow-up _CONFIRM_ request is required, status code has to be parsed.

Code **1000 indicates** that WeChat purchase transactions is completed and **no follow-up request is required**.

    {
        "operation": "PURCHASE",
        "timeStamp": "2019-05-07T12:12:38.177Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "241e578a773a4d869408f43928ddf1fd",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "WECHAT",
                "transactionType": "PURCHASE",
                "id": "776af8e4a4d843129149bdf8b73c08b9",
                "timeStamp": "2019-05-07T12:12:32.9Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ],
                "wechatProviderTransactionId": "f75ab0866f55477cb35a2db5db6bb10d",
                "wechatRate": "691870000",
                "wechatSubMchId": "444917",
                "wechatCashFee": "6919",
                "wechatTimeEnd": "20190507201238",
                "gatewayReference": "573ee979-a265-49b9-b020-27418dbb63ef"
            }
        ],
        "externalId": null,
        "merchantReceiptId": 262,
        "multitender": true
    }

- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1000" means operation is completed successfully
    - **"result"** - "SUCCESS" means operation is completed successfully
- **"id"** - Sale-Purchase identifier assigned by Wirecard ePOS system
- **"externalCashierId"** - relevant for [Advanced Integration](advanced_overview.md); otherwise null
- **"payments"** - specific information for every payment method
    - **"paymentMethod"** - echoed from request
    - **"transactionType"** - echoed from request
    - **"id"** - identifier of purchase transaction assigned by Wirecard ePOS system
    - **"timeStamp"** - date-time when transaction was processed by payment gateway
    - **"statuses"**
        - **"result"** - "SUCCESS" means transaction is completed successfully
        - **"code"** - code "1000" means transaction is completed successfully
        - **"message"** - message provided by payment gateway
    - **"wechatProviderTransactionId"** - transaction identifier in WeChat System
    - **"wechatRate"** - exchange rate between Sale currency and CNY in WeChat System; 691870000 means 6.918
    - **"wechatSubMchId"** - merchant identifier in WeChat System
    - **"wechatCashFee"** - amount in CNY (Chinese Yuan); 6919 means 69.19 CNY
    - **"wechatTimeEnd"** - date-time in WeChat system
    - **"gatewayReference"** - transaction identifier in Wirecard payment gateway
- **"externalId"** - echoed from request
- **"merchantReceiptId"** - unique identifier per merchant; it is incremented with every Sale-Purchase and Sale-Return; advised to be printed on receipt as a barcode
- **"multitender"** - echoed from request

!!! Important
    
    After successful PURCHASE operation, [GET a Sale call](#get-a-sale-call) is advised, as it provides complete Sale information.

### Response indicating 2-step WeChat payment

In order to identify whether the follow-up _CONFIRM_ request is required, status code has to be parsed.

Code **1001 indicates** that WeChat purchase transactions is not completed and **follow-up _CONFIRM_ request is required**.

    {
        "operation": "PURCHASE",
        "timeStamp": "2019-05-07T12:01:24.703Z",
        "status": {
            "code": "1001",
            "result": "SUCCESS"
        },
        "id": "3c9cf14fe82f42bfbecb6dec22edbfe3",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "WECHAT",
                "transactionType": "PURCHASE",
                "id": "9685e8c3620a4c6b8e98518c7b2427d4",
                "timeStamp": "2019-05-07T12:01:24.614Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1001",
                        "message": "Transaction OK."
                    }
                ],
                "wechatSubMchId": "693876",
                "gatewayReference": "c7d76bcf-595d-4318-a9b9-38ac9ac1d53a"
            }
        ],
        "externalId": null,
        "merchantReceiptId": 261,
        "multitender": true
    }
    
- **"operation"** - echoed from request
- **"timeStamp"** - date-time when response was constructed
- **"status"**
    - **"code"** - code "1001" means operation is successful, however follow-up _CONFIRM_ request is required to complete WeChat purchase transaction
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
        - **"code"** - code "1001" means transaction is successful
        - **"message"** - message provided by payment gateway
    - **"wechatSubMchId"** - merchant identifier in WeChat System
    - **"gatewayReference"** - transaction identifier in Wirecard payment gateway
- **"externalId"** - echoed from request
- **"merchantReceiptId"** - unique identifier per merchant; it is incremented with every Sale-Purchase and Sale-Return; advised to be printed on receipt as a barcode
- **"multitender"** - echoed from request

## Confirm Operation

### Request
    
    {
        "operation" : "CONFIRM",
        "originalSaleId" : "3c9cf14fe82f42bfbecb6dec22edbfe3",
        "payments" : [
            {
                "paymentMethod" : "WECHAT",
                "transactionType" : "CONFIRM"
            }
        ]
    }
    
- **"operation"** - defines type of Sale request; "CONFIRM" operation does finish the WeChat Purchase transaction
- **"originalSaleId"** - identifier of original Sale-Purchase
- **"payments"** - payment-specific information; one payment transaction per request is supported
    - **"paymentMethod"** - defines payment method; it must be same as original payment transaction
    - **"transactionType"** - defines type of this transaction; CONFIRM operation must include CONFIRM transaction type
    
### Response

Code **1000** indicates that WeChat purchase transaction is completed successfully.

    {
        "operation": "CONFIRM",
        "timeStamp": "2019-05-07T12:02:24.739Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "3c9cf14fe82f42bfbecb6dec22edbfe3",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "WECHAT",
                "transactionType": "CONFIRM",
                "id": "9685e8c3620a4c6b8e98518c7b2427d4",
                "timeStamp": "2019-05-07T12:02:24.641Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ],
                "wechatProviderTransactionId": "dced92fe6e5042a8856bf8e3dc7c15f8",
                "wechatRate": "691870000",
                "wechatSubMchId": "839907",
                "wechatCashFee": "6919",
                "wechatTimeEnd": "20190507200224",
                "gatewayReference": "ae0d14df-7528-4e5e-b2d6-4393b8c767d9"
            }
        ]
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
    - **"wechatProviderTransactionId"** - transaction identifier in WeChat System
    - **"wechatRate"** - exchange rate between Sale currency and CNY in WeChat System; 691870000 means 6.918
    - **"wechatSubMchId"** - merchant identifier in WeChat System
    - **"wechatCashFee"** - amount in CNY (Chinese Yuan); 6919 means 69.19 CNY
    - **"wechatTimeEnd"** - date-time in WeChat system
    - **"gatewayReference"** - transaction identifier in Wirecard payment gateway

!!! Tip
    See also complete list of Wirecard ePOS Sale [request & response examples](https://switch-test.wirecard.com/mswitch-server/doc/api-doc-sale-examples.html).
    
## GET a Sale Call

You can see below an example of GET a Sale call with excluded _merchant_ and _user_ objects which are going to be described in [Merchant Management](merchant-management.md) and [User Management](user.md) respectively.
    
    GET https://switch-test.wirecard.com/mswitch-server/v1/sales/3c9cf14fe82f42bfbecb6dec22edbfe3?excludeField=merchant&excludeField=user
    
    {
        "id": "3c9cf14fe82f42bfbecb6dec22edbfe3",
        "type": "PURCHASE",
        "status": "COMPLETED",
        "totalAmount": 10,
        "note": null,
        "externalId": null,
        "externalCashierId": null,
        "customerId": null,
        "initialized": "2019-05-07T12:01:24.44Z",
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
                "type": "WECHAT_PURCHASE",
                "id": "9685e8c3620a4c6b8e98518c7b2427d4",
                "status": "COMPLETED",
                "amount": 10,
                "lastUpdated": "2019-05-07T12:02:24.668Z",
                "initialized": "2019-05-07T12:01:24.442Z",
                "message": "The resource was successfully created on WeChat side.\nWas: The resource was successfully created on WeChat side, but password confirmation is needed.",
                "gateway": {
                    "id": "wdEeSimulated",
                    "name": "Wirecard EE Simulated",
                    "type": "WIRECARD_EE_SIMULATED",
                    "url": "http://dummy"
                },
                "gatewayReference": "c7d76bcf-595d-4318-a9b9-38ac9ac1d53a",
                "processedByGateway": "2019-05-07T12:01:24.614Z",
                "wechatProviderTransactionId": "dced92fe6e5042a8856bf8e3dc7c15f8",
                "wechatRate": "691870000",
                "wechatSubMchId": "839907",
                "wechatDeviceInfo": "dell",
                "wechatCashFee": "6919.00",
                "wechatTimeEnd": "20190507200224",
                "autoResolveTransactions": [
            
            ],
                "transactionBarcodeId": "15050011719660761"
            }
        ],
        "location": null,
        "clientInfo": null,
        "merchantReceiptId": 261,
        "cancelledBy": null,
        "shiftId": null,
        "cashRegisterId": null,
        "emailForReceipt": null,
        "emailForReceiptProvided": false,
        "multitender": true
    }