# Sale Model

In this chapter we will cover information needed to understand **Wirecard ePOS Sale Model**.

Wirecard ePOS Sale Model distinguishes two types of Sale:

- **Purchase** - happens when end-consumer purchases goods or services
- **Return**   - happens when end-consumer returns goods back to the retailer

Additionally, Wirecard ePOS allows merchants to divide _Purchase_ total amount to multiple payment transactions. [Multi-tender model](multi-tender.md) provides possibility to use any combination of payment methods.

!!! Note
    
    In payment industry domain terms _multi-tender_, _multi-payment_ and _split-payment_ can be considered as synonyms.
    
    In context of **Wirecard ePOS API** we refer to this functionality as [**Multi-tender model**](multi-tender.md).
    
In the following chapters you will find API requests and responses based on payment method you want to integrate:

- [Cash](cash.md)
- [Card](card.md)
- [Alipay](alipay.md)
- [WeChat Pay](wechat.md)

If you look for integration of multiple payments in one _Sale-Purchase_, then see the [Multi-tender model](multi-tender.md) chapter which includes detailed API examples.

!!! Tip
    
    If you have user account on TEST environment, you can check the received credentials - type them instead of {YourUsername} and {YourPassword} - with following CURL request: 
    
        curl -X GET "https://switch-test.wirecard.com/mswitch-server/v1/info/version" -H "accept: text/plain" -u {YourUsername}:{YourPassword}
    Upon successful authentication, response includes current system version.
