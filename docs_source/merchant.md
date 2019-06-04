This chapter describes merchant-relevant information.

In order to get a merchant details, make a `GET /v1/merchants/{id}` call:

    GET ttps://switch-test.wirecard.com/mswitch-server/v1/merchants/e5869bc0303b4dabbf1e593d619146dc
    
        {
          "id": "e5869bc0303b4dabbf1e593d619146dc",
          "name": "{Name}",
          "createdOn": "2019-04-08T11:49:25.708Z",
          "mccCode": {
            "mcc": 5999,
            "name": "Retail Stores"
          },
          "status": "ENABLED",
          "partner": {
            "id": "1",
            "name": "Wirecard Partner",
            "supportPhone": "+421123456789",
            "supportEmail": "support@example.com",
            "serviceChargeRate": 0,
            "paymentConstraints": [],
            "metadata": []
          },
          "address": {
            "street1": "{Street Address}",
            "street2": null,
            "city": "{City}",
            "postalCode": "{Postal Code}",
            "stateOrProvince": null,
            "country": {
              "numericCode": 276,
              "alpha2code": "DE",
              "alpha3code": "DEU",
              "name": "Germany"
            }
          },
          "phone": "{Contact phone number}",
          "supportPhone": "{Support phone number}",
          "supportEmail": "support@example.com",
          "smsSendingAllowed": false,
          "defaultNetTaxation": false,
          "receiptIncludedSaleItems": true,
          "cashRegistersRequired": false,
          "taxNumber": null,
          "taxCategories": [
            {
              "id": "2f9cc808ebdb4e58933139dc39b21575",
              "name": "Reduced_DE VAT rate",
              "country": {
                "numericCode": 276,
                "alpha2code": "DE",
                "alpha3code": "DEU",
                "name": "Germany"
              },
              "standard": false,
              "taxRates": [
                {
                  "id": "1a4dbb7caf994a1bb203b4d65c8406ef",
                  "value": 7,
                  "validFrom": "2016-06-01"
                }
              ],
              "currentValue": 7
            },
            {
              "id": "5358bb794a4848709987c0b34640c5ad",
              "name": "Standard_DE VAT rate",
              "country": {
                "numericCode": 276,
                "alpha2code": "DE",
                "alpha3code": "DEU",
                "name": "Germany"
              },
              "standard": false,
              "taxRates": [
                {
                  "id": "8c2eb1c0fbf74d51836d3d52dc9793dc",
                  "value": 19,
                  "validFrom": "2016-06-01"
                }
              ],
              "currentValue": 19
            },
            {
              "id": "ec96d2bad4b84d9f9f859c17b6535796",
              "name": "Zero_DE VAT rate",
              "country": {
                "numericCode": 276,
                "alpha2code": "DE",
                "alpha3code": "DEU",
                "name": "Germany"
              },
              "standard": false,
              "taxRates": [
                {
                  "id": "1619f0fa2dc045a092160bb10ad4ab56",
                  "value": 0,
                  "validFrom": "2016-06-01"
                }
              ],
              "currentValue": 0
            }
          ],
          "notifyCallbackUrl": null,
          "defaultCurrency": {
            "number": 978,
            "code": "EUR",
            "name": "Euro",
            "minorUnit": 2
          },
          "configuredCurrencies": [],
          "serviceChargeRate": null,
          "serviceChargeTaxCategory": {
            "id": "ec96d2bad4b84d9f9f859c17b6535796",
            "name": "Zero_DE VAT rate",
            "country": {
              "numericCode": 276,
              "alpha2code": "DE",
              "alpha3code": "DEU",
              "name": "Germany"
            },
            "standard": false,
            "taxRates": [
              {
                "id": "1619f0fa2dc045a092160bb10ad4ab56",
                "value": 0,
                "validFrom": "2016-06-01"
              }
            ],
            "currentValue": 0
          },
          "tipTaxCategory": {
            "id": "ec96d2bad4b84d9f9f859c17b6535796",
            "name": "Zero_DE VAT rate",
            "country": {
              "numericCode": 276,
              "alpha2code": "DE",
              "alpha3code": "DEU",
              "name": "Germany"
            },
            "standard": false,
            "taxRates": [
              {
                "id": "1619f0fa2dc045a092160bb10ad4ab56",
                "value": 0,
                "validFrom": "2016-06-01"
              }
            ],
            "currentValue": 0
          },
          "flatDiscount": null,
          "productStockEnabled": false
        }