This chapter describes how can merchant manage its shops.

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
        "externalId": "{externalId}",
        "siteId": "{siteId}",
        "status": "ENABLED"
    }
    
- `"name"` - _optional field_ - shop name
- `"address"` - shop address
    - `"city"`
    - `"country"` - defined by `alpha2code` which is two-letter country code; see [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
    - `"postalCode"`
    - `"stateOrProvince"` - _optional field_
    - `"street1"`
    - `"street2"` - _optional field_
- `"externalId"` - _optional field_ - needed for ERP integration
- `"siteId"` - _optional field_ - needed for ERP integration
- `"status"` - either `ENABLED` or `DISABLED`

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
        "externalId": "{externalId}",
        "siteId": "{siteId}",
        "status": "ENABLED"
    }

## List all shops

In order to list all shops, make a `GET /v1/merchants/{merchantId}/shops` call.

## Get a shop

In order to list a specific shop, make a `GET /v1/merchants/{merchantId}/shops/{shopId}` call.


