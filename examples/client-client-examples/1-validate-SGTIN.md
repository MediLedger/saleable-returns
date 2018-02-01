## Validate a SGTIN

Before a distributor can legally resell a shipment of product, it needs to verify the product based on SGTIN, lot number, and expiration date. The first step involves discovering the verification service pertaining to that GTIN. This is done using the MediLedger Blockchain as exemplified [here](../smart-contract-examples/3-Gtin-Lookup.md).

Once the distributor has identified the verification service, it uses a client-to-client communication channel to validate the product. This endpoint triggers a local-only lookup of the SGTIN with the specified properties in the serialization repository. If the combination of SGTIN, lot number and expiration date is not found, a response will be sent indicating that the product could not be found. If it is found, the client will return the SGTIN, lot number and expiration date and the distributor has received the legally required confirmation of validity.

	POST /api/2.0/asset/:sgtin_uri/validation


### Parameters

| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| sgtin_uri | String | <p>A URI that represents the SGTIN of an Asset</p>|

### Request Body

| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| properties | Object | <p>The properties of the asset to be validated</p>|

### Examples

Example Usage

```
curl --request POST \
--url https://api.chronicled.com/api/2.0/asset/urn:epc:id:sgtin:01234.56789.10111213/verification \
-H 'Authorization: Bearer $JWT' \
--data '{
   "properties": {
     "Lot Number": "1",
     "Expiration Date": "01/01/2018"
   }
 }'
```

### Success 200

| Name     | Type       | Description                           |
|:---------|:-----------|:--------------------------------------|
| created_at | Date | <p>Marks the time that the validation was performed</p>|
| sgtin_uri | String | <p>The URI that identifies the SGTIN of the Asset that was validated</p>|
| valid | Boolean | <p>The result of the validation. If true, all the properties matched the Asset. If false, one or more of the properties did not match or could not be confirmed.</p>|
| properties | Object | <p>The properties that were supplied in the request and checked against the Asset</p>|


### Success Response

Successful Response

```
{
  "created_at":"2016-08-05T20:39:33.234Z",
  "valid": true,
  "sgtin_uri": "urn:epc:id:sgtin:01234.56789.10111213",
  "properties": {
    "Lot Number": "1",
    "Expiration Date": "01/01/2018"
  }
}
```
