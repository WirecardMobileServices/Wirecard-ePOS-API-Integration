_REVERSE_ operation is typically used in case Purchase, Terminal Authorization or Capture transaction was created accidentally and hence needs to be reversed.

## Reverse Operation

In order to reverse Purchase, Terminal Authorization or Capture transaction, make a<br/>[`POST /v1/sales`](https://switch.wirecard.com/mswitch-server/v1/sales) call:

### Request

    {
        "operation": "REVERSE",
        "originalSaleId": "a2c6d5fb0025474bbfd60256c5386c47",
        "note": "ReverseNote",
        "payments": [
            {
                "paymentMethod": "CARD",
                "transactionType": "REVERSAL",
                "originalTransactionId": "853f09aff023495b89a072638cb93c65"
            }
        ]
    }

- `"operation"` - defines type of Sale request
- `"originalSaleId"` - identifier of original Sale-Purchase
- `"payments"` - includes payment-specific information
    - `"paymentMethod"` - defines payment method; must be same as original payment method
    - `"transactionType"` - defines type of transaction; `REVERSE` operation must include `REVERSAL` transaction type
    - `"originalTransactionId"` - identifier of original Card Purchase transaction which will be reversed

### Response

    {
        "operation": "REVERSE",
        "timeStamp": "2019-08-28T13:51:22.677Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "a2c6d5fb0025474bbfd60256c5386c47",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "CARD",
                "transactionType": "REVERSAL",
                "id": "1d4900351ebc44c3838d9b4d8cf0be3b",
                "timeStamp": "2019-08-28T13:51:22.639Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ],
                "authorizationCode": "889456"
            }
        ]
    }

- `"operation"` - echoed from request
- `"timeStamp"` - date-time when response was constructed
- `"status"`
    - `"code"` - `"1000"` means operation is successful
    - `"result"` - `"SUCCESS"` means operation is successful
- `"id"` - identifier of original Sale-Purchase, echoed from request
- `"externalCashierId"` - relevant for [Advanced Integration](advanced-overview.md); otherwise null
- `"payments"` - includes payment-specific information
    - `"paymentMethod"` - echoed from request
    - `"transactionType"` - echoed from request
    - `"id"` - identifier of reversal transaction assigned by Wirecard ePOS system
    - `"timeStamp"` - date-time when transaction was processed
    - `"statuses"`
        - `"result"` - `"SUCCESS"` means transaction is successful
        - `"code"` -  `"1000"` means transaction is successful
        - `"message"` - message provided by payment gateway
    - `"authorizationCode"`- authorization code provided by scheme
    
In order to explicitly [change state of Sale-Purchase to CANCELED](multi-tender.md#what-is-sale-lifecycle-model), make a  `POST /v1/sales` call with [_CANCEL_ operation](multi-tender.md#what-is-cancel-operation).

!!! Tip
    To see all `/v1/sales` request & response examples, [click here](https://switch-test.wirecard.com/mswitch-server/doc/api-doc-sale-examples.html).