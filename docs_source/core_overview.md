At the core of Wirecard ePOS solution is payment acceptance. This chapter provides all information in order to successfully process **Payment Transaction**.

!!! Note
    
    **Payment Transaction** (also called payment) is a monetary transaction with specific _amount_, _payment method_ and _type_.
    
In context of Wirecard ePOS, every Payment Transaction is part of [**Sale**](sale-general.md).

!!! Note

    **Sale** is central ePOS object. It must contain _amount_ to pay and at least one _payment transaction_. Additionally, Sale may include _sale items_ (also called shopping basket), reference to _merchant shop_, reference to _cash register_ and other optional sale information.

Wirecard ePOS allows merchants to pay Sale total amount by multiple payments. It is possible to use any combination of payment methods.

    
Wirecard ePOS supports following **payment methods**:
    
- [Cash](cash.md)
- [Card](card.md) (EMV/Magstripe)
- [Alipay](alipay.md) (barcode payment)
- [WeChat](wechat.md) (barcode payment)

!!! Note
     
     Accepted card schemes are **VISA** and **Mastercard**.
     
     **American Express**, **UnionPay International** and **JCB** card schemes are coming soon.