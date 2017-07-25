# Offer API documentation

Provides details of an loyalty offer.

## Usage Requirement

You must first create your application in the developer portal. Then you can register your application to this API. After registering, you receive an application key; you mush pass this key in an    
    **X-API-Key**   
header with the request. Request not including this header or a valid key will be rejected.

## Rate Limit

This API is limited to five request per minute. Requests exceeding this thershod are **rejected**.

## Required Headers

| Header | Value |
| -- | -- |
| X-API-Key | Key provided with application registration |

## GET Offer

Returns offer details for the provided offer ID

**Resource URL**: `https://<hostname>/apis/v1/offers/{offerid}`

**Example Request**:
```bash
   curl -X GET -H "X-API-Key: 29013cc1-667d-4db4-96d8-cc3ee0c4deb2" \
     https://api.orcl.asia/apis/v1/offers/10001
```

**Example Response**
```json
{
  "id":10001,
  "name":"Our new aroma roast",
  "points":10000,
  "message":"Try special brew today and enjoy 10% off with 10,000 points",
  "productid":20001,
  "productname":"Aroma Beans",
  "productprice":21,
  "productimage":"20001.jpg",
  "productdesc":"Blend of incomparable Balance of sweetness, aroma and body. Composed of 50% Arabica and 50% Robusta."
}
```
