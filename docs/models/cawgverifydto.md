# CawgVerifyDto

Options controlling CAWG identity validation behavior during verification.


## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `validate_`                                                       | *Optional[bool]*                                                  | :heavy_minus_sign:                                                | Whether to run CAWG identity validation.                          |
| `require_valid_identity`                                          | *Optional[bool]*                                                  | :heavy_minus_sign:                                                | Whether to fail verification if CAWG identity is missing/invalid. |