## Creating ABC Corp

The following code snippets can be used to create and get information for a manufacturer on the blockchain. These use the *CompanyDirectory.sol* (soon to be published) smart contract.

Assuming we have the contract's ABI and deployed address, we can construct the `CompanyDirectory` as following using `web3.js`:

```
const CompanyDirectory = web3.eth.contract(CompanyDirectoryABI).at(deployedAddress);
```

#### 1. Register ABC Corp

The MediLedger Blockchain registers new manufacturers with the following function.

```
CompanyDirectory.register(
  ["0x6773313a636f6d70616e795f707265666978"],
  ["0x0123"],
  "ABC Corp",
  "0x1",
  "0x4b0897b0513fdc7c541b6d9d7e929c4e5364d2db"
)
```
The following event is triggered by the successful execution of the function above:

```
CompanyRegistered(
  ["0x6773313a636f6d70616e795f707265666978000"]
  ["0x012300000000000000000000000000000000000"],
  "ABC Corp",
  "0x1000000000000000000000000000000000000000",
  "0x4b0897b0513fdc7c541b6d9d7e929c4e5364d2db"
)
```
#### 2. Set security certificate for ABC Corp

This can only be set by the company that owns the certificate (i.e. ABC Corp this case):
```
CompanyDirectory.setCertificate("0x23AF.........................................9AE")
```
The following event is triggered by the successful execution of the above function:

```
CertificateUpdated(
  "0x6773313a636f6d70616e795f7072656669780000",
  "0x0123000000000000000000000000000000000000",
  "0x23AF.........................................9AE"
)
```

#### 3. Add/Update Endpoint
These functions can only be called by the company that owns the endpoint (i.e. ABC Corp in this case):
```
CompanyDirectory.addEndpoint(
  "0x3F3AC68",
  "www.abc_corp.com/verifyURL"
)
CompanyDirectory.updateEndpoint(
  "0x3F3AC68",
  "www.abc_corp.com/updated_verifyURL"
)
```
The following events are triggered by each of the above functions upon successful execution:

```
EndpointCreated(
  "0x6773313a636f6d70616e795f7072656669780000",
  "0x0123000000000000000000000000000000000000",
  "0x3F3AC68000000000000000000000000000000000",
  "www.abc_corp.com/verifyURL"
)

EndpointUpdated(
  "0x6773313a636f6d70616e795f7072656669780000",
  "0x0123000000000000000000000000000000000000",
  "0x3F3AC68000000000000000000000000000000000",
  "www.abc_corp.com/updated_verifyURL",
)
```

#### 4. Test whether ABC Corp and endpoint 1 successfully created

```
CompanyDirectory.companyExists("0x6773313a636f6d70616e795f7072656669780000", "0x0123")     // returns bool

CompanyDirectory.getEndpointUrl("0x6773313a636f6d70616e795f7072656669780000", "0x0123", "0x1") // call with identity id, returns "www.abc_corp.com/updated_verifyURL"
```

## 5. Create XYZ Corp

Like step 1, create XYZ Corp on the blockchain. Use the following arguments for this demo script:

XYZ Corp:

| Argument      | Value         |
| ------------- |-------------|
|Company prefix | 0789|
|Name | XYZ Corp |
|Permission| 1 |
|Address| 0xdd870fa1b7c4700f2bd7f44238821c26f7392148 |
|Certificate data| test_data |
|End point url | www.xyz_corp.com/verify   (corresponds to id = 2) |

