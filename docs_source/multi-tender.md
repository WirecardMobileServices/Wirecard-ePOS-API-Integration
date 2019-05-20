Wirecard ePOS solution offers buyers opportunity to divide Sale total amount to multiple payment transactions.

!!! Example
    Jeans in value of 100 € are paid by two payment transactions: 60 € is paid by _card_ and 40 € is paid in _cash_.

## Why Wirecard ePOS supports multi-tender?
    
Simple. Merchant is able to increase its revenue as the likelihood to reach more end-consumers is increasing with more payment options provided.

End-consumers may want to combine multiple debit and/or credit cards, especially in case of purchases in value of thousands Euro which exceeds the limits on their cards.

## How to integrate multi-tender?

Simple. As long as the **"multitender"** flag in the Sale PURCHASE request is **true**, you are integrated.

!!! Warning

    It is strongly advised to send **"multitender": "true"**, so you are compliant with the current [Sale lifecycle model](#what-is-sale-lifecycle-model). Otherwise, you are integrated with deprecated Sale lifecycle model.

## How to make multi-tender Sale?

Let's go through real-live example below.

!!! Example

    Imagine a sale when watches in value of 10 000 € are paid by two Alipay transactions, each in value of 5 000 €.

    **Initial Sale PURCHASE Request:**
    
        {
            "multitender": "true",
            "operation" : "PURCHASE",
            "totalAmount" : 10000,
            "currencyCode" : "EUR",
            "payments" : [
                {
                    "paymentMethod" : "ALIPAY",
                    "transactionType" : "PURCHASE",
                    "amount" : 5000,
                    "consumerId" : "28050011747660761"
                }
            ]
        }
    
    **Sale REFERENCE_PURCHASE Request:**
    
        {
            "operation" : "REFERENCE_PURCHASE",
            "originalSaleId": "5d01cf38548f4007962e7d68004fcc76",
            "payments" : [
                {
                    "paymentMethod" : "ALIPAY",
                    "transactionType" : "PURCHASE",
                    "amount" : 5000,
                    "consumerId" : "28050011747612989"
                }
            ]
        }
     
    For sake of overview, responses are not provided. See [Alipay page](alipay.md#response) for detailed PURCHASE response.
    
## What is Sale lifecycle model?

