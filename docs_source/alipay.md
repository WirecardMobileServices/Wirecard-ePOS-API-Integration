Alipay barcode payment is one-step payment method what means that only one request to Wirecard ePOS API is needed.

!!! Tip

    For more details regarding Alipay, visit [Wirecard China Payment](https://www.wirecard.com/chinapayment/en/) website.


!!! Note
    
    Sale requests are serviced at https://switch.wirecard.com/mswitch-server/v1/sales URL.

**Request**
    
    {
        "multitender": "true",
        "operation" : "PURCHASE",
        "totalAmount" : 10,
        "currencyCode" : "EUR",
        "payments" : [
            {
                "paymentMethod" : "ALIPAY",
                "transactionType" : "PURCHASE",
                "amount" : 10,
                "consumerId" : "28050011719660761"
            }
        ]
    }
    
**Response**

    {
        "operation": "PURCHASE",
        "timeStamp": "2019-04-10T09:36:46.966Z",
        "status": {
            "code": "1000",
            "result": "SUCCESS"
        },
        "id": "df6002b920934666af20baea475b33c4",
        "externalCashierId": null,
        "payments": [
            {
                "paymentMethod": "ALIPAY",
                "transactionType": "PURCHASE",
                "id": "c0027741b70e410988cab79e837baad3",
                "timeStamp": "2019-04-10T09:36:24Z",
                "statuses": [
                    {
                        "result": "SUCCESS",
                        "code": "1000",
                        "message": "Transaction OK."
                    }
                ],
                "alipayPayTime": "20190410093623816",
                "alipayTransId": "1554888983816",
                "alipayBuyerLoginId": "api***@163.com",
                "exchangeRate": 6.5228,
                "transAmountCny": 65.23,
                "merchantName": "MA-09093587-8cb4-402f-9edc-7ba8dfaecffc",
                "terminalId": "1234567",
                "gatewayReference": "7986c4ca-449b-4cbb-bb90-a53605e61607"
            }
        ],
        "externalId": null,
        "merchantReceiptId": 456,
        "multitender": true
    }