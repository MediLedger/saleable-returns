## Get Lookup Directory

Each VRS needs to maintain a Lookup Directory (LD) that maps a GTIN to the VRS of the GTIN's manufacturer. This would enable correctly routing an SGTIN request to the relevant VRS for verification. To enable updates in the LD of MediLedger to propagate across other VRSs, the MediLedger gateways offer the following endpoints:

- [Get LD Entries](#get-ld-entries)
- [Get LD Entry By ID](#get-ld-entry-by-id)

#### Get LD Entries

`GET /api/2.0/ld-entry`

<p>This endpoint is used in client-to-client communications to see existing entries in the Lookup Directory</p>

###### Request Query Parameters
| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| prefix_owner	**optional**	| String	|  <p>Filters the results to those that match the prefix owner supplied</p>		|
| start	**optional**	| Number	|  <p>Filters the results to those whose &quot;created_on&quot; date are on or after the start date as a Unix timestamp</p>		|
| end	**optional**	| Number	|  <p>Filters the results to those whose &quot;created_on&quot; date are on or before the end date as a Unix timestamp</p>		|
| hostname	**optional**	| String	|  <p>Filters the results to those that match the hostname</p>		|


###### HTTP Request

> Example Usage

```shell
curl --request GET \
--url https://api.chronicled.com/api/2.0/ld-entry?prefix_owner=01234&start=1518218471091
-H 'Authorization: Bearer $JWT' \
```


###### Success Fields

| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| ld-entries 	| Object[]	|  <p>An array of objects corresponding to the entries in the client's Lookup Directory</p>	|
| - .uris 	| String[]	|  <p>The URIs of the LD entry, one of which will contain the GTIN encoded as a valid GS1 element string</p>	|
| - .gtin 	| String	|  <p>The raw GTIN that was submitted. Can be a GTIN-14, GTIN-13, GTIN-12, or GTIN-8</p>	|
| - .prefix_owner 	| String	|  <p>The company prefix of the Organization that owns the GTIN</p>	|
| - .hostname 	| String	|  <p>The host to query when validating SGTIN's that ar composed of this GTIN</p>	|
| - .external 	| Boolean	|  <p>Boolean which indicates whether or not the LD entry created contains a hostname external to the MediLedger network</p>	|

> Successful Response

```json
[
  {
    "created_at":"2017-02-10T20:39:33.234Z",
    "uris": ["gs1:es:0101234567890124"]
    "gtin": "01234567890123",
    "prefix_owner": "01234"
    "hostname": "external.company.com"
    "external": ture
  }
]
```

#### Get LD Entry by ID

`GET /api/2.0/ld-entry/:uri`

<p>This endpoint is used in client-to-client communications to see an existing entry in the Lookup Directory by one of its identifiers</p>

###### Parameters
| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| uri		| String	|  <p>The URI of the entry in the Lookup Directory</p> |


###### HTTP Request

> Example Usage

```shell
curl --request GET \
--url https://api.chronicled.com/api/2.0/ld-entry/gs1:es:0101234567890123
-H 'Authorization: Bearer $JWT' \
```


###### Success Fields
> Successful Response


| Name    | Type      | Description                          |
|---------|-----------|--------------------------------------|
| uris 	| String[]	|  <p>The URIs of the LD entry, one of which will contain the GTIN encoded as a valid GS1 element string</p>	|
| gtin 	| String	|  <p>The raw GTIN that was submitted. Can be a GTIN-14, GTIN-13, GTIN-12, or GTIN-8</p>	|
| prefix_owner 	| String	|  <p>The company prefix of the Organization that owns the GTIN</p>	|
| hostname 	| String	|  <p>The host to query when validating SGTIN's that ar composed of this GTIN</p>	|
| external 	| Boolean	|  <p>Boolean which indicates whether or not the LD entry created contains a hostname external to the MediLedger network</p>	|


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
