# CawgIdentityDto

Configuration to add a CAWG identity assertion during signing. Presence of this object enables CAWG.


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `signer`                                                       | [Optional[models.Signer]](../models/signer.md)                 | :heavy_minus_sign:                                             | N/A                                                            |
| `signing_alg`                                                  | [Optional[models.SigningAlg]](../models/signingalg.md)         | :heavy_minus_sign:                                             | Algorithm used for the CAWG identity signature.                |
| `referenced_assertions`                                        | List[*str*]                                                    | :heavy_minus_sign:                                             | Assertion labels that the identity assertion should reference. |
| `timestamper`                                                  | *Optional[str]*                                                | :heavy_minus_sign:                                             | Timestamper to use ("digicert" or "custom:<url>").             |