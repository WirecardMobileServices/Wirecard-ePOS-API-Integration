At the core of Wirecard ePOS solution is payment processing.

_Core Integration_ chapter provides basic information in order to successfully process **Payment Transaction**.

!!! Note
    
    **Payment Transaction** (also called payment) is a monetary transaction with specific _amount_, _payment method_ and _type_.
    
In context of Wirecard ePOS, every Payment Transaction is part of **Sale**:

- **Purchase** record (also called Sale-Purchase) is created when end-consumer purchases goods.
- **Return** record (also called Sale-Return) is created when end-consumer returns purchased goods back to merchant.

!!! Important

    **Sale** is central ePOS object. It must contain _amount_ to pay and at least one _payment transaction_.
    
    Additionally, Sale may include _sale items_ (aka shopping basket), reference to _merchant shop_, reference to _cash register_ and other optional sale-related information.

Wirecard ePOS supports following **payment methods**:
    
- [Cash](cash.md)
- [Card](card.md) (EMV/Magstripe)
- [Alipay](alipay.md) (barcode payment)
- [WeChat](wechat.md) (barcode payment)

On top of traditional payment processing, Wirecard ePOS provides option to [divide Sale total amount](multi-tender.md) to multiple payment transactions.

!!! Example
    Jeans in value of 100 € are paid by two payment transactions: 60 € is paid by _card_ and 40 € is paid in _cash_.