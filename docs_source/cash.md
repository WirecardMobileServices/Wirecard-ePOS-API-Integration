The simplest payment method is cash. It is one-step payment method what means that only one request to Wirecard ePOS API is needed.

**Request**
    
    POST /v1/sales
    
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
    
  