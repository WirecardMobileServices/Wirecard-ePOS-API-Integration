#Card Payment

No two businesses are alike, but all of them need to accept payments. With Wirecard ePOS solution, companies of all sizes can accept and process card payments anywhere ― quickly, securely, and profitably.

!!! Tip

    Visit [Wirecard website](https://www.wirecard.com/payment-base/pos) to find out all benefits of accepting card payments.

## Transaction Types

Wirecard ePOS supports following transaction types:

- **[Purchase](card-purchase-flow.md)** - takes funds from the cardholder's account. It is one-step process to conduct two transaction types: Authorization and Capture.
- **[Authorization & Capture](card-auth-flow.md)** - Authorization reserves funds from the cardholder's account. Merchant has 7 days left to conduct Capture on the Authorization transaction.
- **[Reversal](card-reversal-flow.md)** - releases reserved funds from the cardholder's account. It is used to solve specific situations, e.g. in case when a Purchase, Authorization or Capture transaction was triggered accidentally.
- **[Reference Refund](card-reference-refund-flow.md)** - gives funds to the cardholder's account. It has to refer to an eligible Purchase or Capture transaction.

!!! Note
    
    Sale requests are serviced at following URL:
    
        https://switch.wirecard.com/mswitch-server/v1/sales

    In context of Wirecard ePOS, term `Purchase` is used for both:
    
    - type of Sale - called _Sale-Purchase_ - created by request with PURCHASE operation
    - transaction type - _Cash Purchase_ transaction, _Card Purchase_ transaction, _Alipay Purchase_ transaction and _WeChat Purchase_ transaction
