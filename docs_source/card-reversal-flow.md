Reverse operation is typically used in case Purchase, Terminal Authorization or Capture transaction was created accidentally and hence needs to be reversed.

## Reverse Operation

In order to reverse Purchase, Terminal Authorization or Capture transaction, make a [`POST /v1/sales`](https://switch.wirecard.com/mswitch-server/v1/sales) call:

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
