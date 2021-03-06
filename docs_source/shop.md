This chapter describes how can merchant manage its shops. Merchant is then able to reference shop (via `shopId`) in the Sale requests.

## Create new shop

In order to create new shop, make a `POST /v1/merchants/{merchantId}/shops` call:

### Request

    {
        "name": "{shopName}",
        "address": {
            "city": "{city}",
            "country": {
                "alpha2code": "DE"
            },
            "postalCode": "{postalCode}",
            "stateOrProvince": "{stateOrProvince}",
            "street1": "{street1}",
            "street2": "{street2}"
        },
        "status": "ENABLED"
    }
    
Both `stateOrProvince` and `street2` are optional fields.

### Response

    {
        "id": "8397fa0dea7546f2986105bd3681a6b7",
        "name": "{shopName}",
        "address": {
            "street1": "{street1}",
            "street2": "{street2}",
            "city": "{city}",
            "postalCode": "{postalCode}",
            "stateOrProvince": "{stateOrProvince}",
            "country": {
                "numericCode": 276,
                "alpha2code": "DE",
                "alpha3code": "DEU",
                "name": "Germany"
            }
        },
        "merchant": { ...
        },
        "externalId": null,
        "siteId": null,
        "status": "ENABLED"
    }

## List all shops

In order to list all shops, make a `GET /v1/merchants/{merchantId}/shops` call.

## Get a shop

In order to list a specific shop, make a `GET /v1/merchants/{merchantId}/shops/{shopId}` call.


