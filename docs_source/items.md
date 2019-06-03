This chapter describes Sale items which can be considered as shopping basket. Items include information about the goods and services sold by merchant.

!!! Example

    `POST /v1/sales` call:
    
        "operation" : "PURCHASE",
        ...
        "totalAmount" : 18.8,
        "items": [
            {
                "type": "PURCHASE",
                "description": "Cofee cup",
                "itemTotal": 18.0,
                "quantity": 2.0,
                "unitPrice": 10.0,
                "unitPriceModified": 9.0,
                "unitTax": 20.0,
                "internalProductId": "9135c64878d911e680a8ecf4bb60cfe0",
                "externalProductId": "MC12345",
                "categoryName":"Cups",
                "externalCategoryId":"TS-02154"
            },
            {
                "type": "SERVICE_CHARGE",
                "description": "SERVICE_CHARGE",
                "itemTotal": 0.8,
                "quantity": 1.0,
                "unitPrice": 0.8,
                "unitTax": 20.0
            }
        ],
        "unitPricesIncludeTax": true
        ...
        
Item may include following fields:

- `"type"` - type of the item, can be one of:
    - `"PURCHASE"` - it is a standard type used when end-consumer purchase goods and/or services
    - `"SERVICE_CHARGE"` - it is an additional "fee" added to end-consumer bill for the service of providing goods and/or services; service charge base is calculated from Sale Items Net Totals and then taxed by configured merchant’s tax value
    - `"TIP"` - it is a gratuity paid by end-consumer; tip amount is always considered as an amount with tax, regardless of `unitPricesIncludeTax` parameter setting
- `"description"` - item description
- `"itemTotal"` - total price; sum of all `itemTotal` has to be equal to `totalAmount`, `itemTotal` has to be equal to `unitPrice` * `quantity`
- `"quantity"` - ordered quantity
- `"unitPrice"` - unit price
- `"unitPriceModified"` - _optional field_ - discounted price; when it is present, then system considers this price instead of `unitPrice`
- `"unitTax"` - tax applied
- `"internalProductId"` - identifier of the product in Wirecard ePOS system; _mandatory field_ in case i) Authorize or Capture transaction types are used, or ii) merchant wants to utilise Product Stock tracking
- `"externalProductId"` - _optional field_ - identifier of the product in external system
- `"categoryName"` - _optional field_ - category name that the item was selected from
- `"externalCategoryId"` - _optional field_ - external category ID that the item was selected from

Together with item, parameter `"unitPricesIncludeTax"` (boolean) indicates whether unit prices already includes tax.