## Transfer ownership of GTIN 1 from ABC Corp to XYZ Corp

#### 1. Initiate transfer by ABC Corp

Only ABC Corp (i.e. the current owner of GTIN 1) can initiate the transfer.

```
  GtinDirectory.initTransfer(
    "0x00006789123456",
    "0x0788"
  )
```

#### 2. Accept transfer by XYZ Corp

Only XYZ Corp (i.e. the destination company) can accept the transfer. Moreover, XYZ Corp should own the endpoint ID supplied below.

```
  GtinDirectory.acceptTransfer(
    "0x00006789123456",
    "0x128D93B",
    "www.abc_corp.com/updated_verifyURL"
  )
```

Successful execution triggers the following event.

```
  Transferred(
    "0x0000678912345600000000000000000000000000",
    "0x0788000000000000000000000000000000000000",
    "0x128D93B000000000000000000000000000000000",
  )
```
