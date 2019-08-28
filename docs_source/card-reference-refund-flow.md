## Return Operation

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
        ],
        "validateCashReturn": true
    }

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