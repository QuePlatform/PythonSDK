# Data

The trust list data containing certificates and policies.


## Fields

| Field                                                                               | Type                                                                                | Required                                                                            | Description                                                                         |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `manufacturers`                                                                     | List[*str*]                                                                         | :heavy_check_mark:                                                                  | List of trusted hardware manufacturers whose devices can create trusted provenance. |
| `cas`                                                                               | List[*str*]                                                                         | :heavy_check_mark:                                                                  | List of trusted Certificate Authority certificates in PEM format.                   |
| `policy`                                                                            | [models.Policy](../models/policy.md)                                                | :heavy_check_mark:                                                                  | Trust policy configuration defining default trust behavior.                         |