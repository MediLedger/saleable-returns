## Create an LD Entry

`POST /api/2.0/ld-entry`

<p>This endpoint is used in client-to-client communications to add an additional entry to the client's Lookup Directory. This addition is then propagated to all clients within the MediLedger using the blockchain. Each entry in the Lookup Directory should host a GTIN that is used for making SGTINs and a hostname that provides a location to verify SGTINs created with this GTIN. The presence of the <code>external</code> field indicates whether or not the host exists inside or outside of the MediLedger network. Entries that exist outside of the MediLedger network will need to route traffic through a gateway.</p>

### Request Body
| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| gtin		| String	|  <p>The GTIN that is being added. Supports GTIN-14, GTIN-13, GTIN-12, and GTIN-8 encodings</p>		|
| prefix_owner		| String	|  <p>The company prefix of the Organization that owns the GTIN</p>		|
| hostname		| String	|  <p>The host to query when validating SGTIN's that are composed of this GTIN</p>		|

### HTTP Request

> Example Usage

```shell
curl --request POST \
--url https://api.chronicled.com/api/2.0/ld-entry \
-H 'Authorization: Bearer $JWT' \
--data '{
   "gtin": "01234567890123",
   "prefix_owner": "01234"
   "hostname": "external.company.com"
 }'
```
### Success Fields

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| uris 	| Date	|  <p>The URIs of the new LD entry, one of which will contain the GTIN encoded as a valid GS1 element string</p>	|
| gtin 	| String	|  <p>The raw GTIN that was submitted. Can be a GTIN-14, GTIN-13, GTIN-12, or GTIN-8</p>	|
| prefix_owner 	| Boolean	|  <p>The company prefix of the Organization that owns the GTIN</p>	|
| hostname 	| Object	|  <p>The host to query when validating SGTIN's that ar composed of this GTIN</p>	|
| external 	| Boolean	|  <p>Boolean which indicates whether or not the LD entry created contains a hostname outside of the network. Will always be true for LD entries created through this endpoint</p>	|

> Successful Response

```json
{
  "created_at":"2016-08-05T20:39:33.234Z",
  "uris": ["gs1:es:0101234567890123"]
  "gtin": "01234567890123",
  "prefix_owner": "01234"
  "hostname": "external.company.com"
  "external": ture
}
```
