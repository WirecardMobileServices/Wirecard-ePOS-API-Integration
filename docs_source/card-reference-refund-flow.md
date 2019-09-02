_RETURN_ operation is used in case end-consumer returns merchandise and asks for a refund. Wirecard ePOS support partial as well as full return.

## Return Operation

In order to process Alipay refund transaction, make a [`POST /v1/sales`](https://switch.wirecard.com/mswitch-server/v1/sales) call defined below:

### Request

    {
        "operation": "RETURN",
        "note": "ReturnNote",
        "externalId": "987654321",
        "totalAmount": 10,
        "currencyCode": "EUR",
        "originalSaleId": "8b7109783ce04de9bfb88ce1e30ad399",
        "payments": [
            {
                "paymentMethod": "CARD",
                "transactionType": "REFERENCE_REFUND",
                "amount": 10,
                "originalTransactionId": "56eb1e007d9e4ed78ea433322f8cc04c"
            }
        ]
    }
    
- `"operation"` - defines type of Sale request; `RETURN` operation creates new Sale-Return record
- `"note"` - _optional field_ - used for merchant tracking purposes
- `"externalId"` - _optional field_ - used for merchant tracking purposes
- `"totalAmount"` - defines amount to be refunded; it can be equal (full return) or less (partial return) than total amount in original Sale-Purchase
- `"currencyCode"` - must be same as for original Sale-Purchase
- `"originalSaleId"` - identifier of original Sale-Purchase
- `"payments"` - includes payment-specific information
    - `"paymentMethod"` - defines payment method
    - `"transactionType"` - defines type of transaction; must be `REFERENCE_REFUND` when payment method is `CARD`
    - `"amount"` - defines amount to be refunded; must be same as `totalAmount`
    - `"originalTransactionId"` - identifier of original Card purchase transaction which will be refunded

### Response

    {
        "operation": "RETURN",
        "timeStamp": "2019-08-28T13:55:23.871Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "20cf4d61e49c411ea98908f434383cc0",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "CARD",
                "transactionType": "REFERENCE_REFUND",
                "id": "b153442a213948daa0a689fa1eb23516",
                "timeStamp": "2019-08-28T13:55:23.771Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ],
                "authorizationCode": ""
            }
        ],
        "externalId": "987654321",
        "merchantReceiptId": 344
    }
    
- `"operation"` - echoed from request
- `"timeStamp"` - date-time when response was constructed
- `"status"`
    - `"code"` - `"1000"` means operation is successful
    - `"result"` - `"SUCCESS"` means operation is successful
- `"id"` - Sale-Return identifier assigned by Wirecard ePOS system
- `"externalCashierId"` - relevant for [Advanced Integration](advanced-overview.md); otherwise null
- `"payments"` - includes payment-specific information
    - `"paymentMethod"` - echoed from request
    - `"transactionType"` - echoed from request
    - `"id"` - identifier of refund transaction assigned by Wirecard ePOS system
    - `"timeStamp"` - date-time when transaction was processed
    - `"statuses"`
        - `"result"` - `"SUCCESS"` means transaction is successful
        - `"code"` - `"1000"` means transaction is successful
        - `"message"` - message provided by payment gateway
    - `"authorizationCode"` - authorization code provided by scheme
- `"externalId"` - echoed from request
- `"merchantReceiptId"` - unique identifier for merchant; it is incremented with every Sale-Purchase and Sale-Return; it is advised to be printed on receipt as a barcode

!!! Tip
    To see all `/v1/sales` request & response examples, [click here](https://switch-test.wirecard.com/mswitch-server/doc/api-doc-sale-examples.html).