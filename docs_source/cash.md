The simplest payment method to integrate is cash. It is one-step payment method what means that only one request to Wirecard ePOS API is needed.

!!! Note
    
    Sale requests are serviced at https://switch.wirecard.com/mswitch-server/v1/sales URL.

**Request**
    
    {
        "multitender": "true",
        "operation" : "PURCHASE",
        "note": "My First Sale",
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

**Response**

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