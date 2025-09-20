# TrustListResponse

The current C2PA trust list containing trusted certificate authorities, hardware manufacturers, and trust policies used for manifest verification.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `version`                                                            | *str*                                                                | :heavy_check_mark:                                                   | Version identifier for this trust list bundle.                       | dev-1                                                                |
| `issued_at`                                                          | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | Timestamp when this trust list was issued.                           | 2024-01-15T10:00:00Z                                                 |
| `data`                                                               | [models.Data](../models/data.md)                                     | :heavy_check_mark:                                                   | The trust list data containing certificates and policies.            |                                                                      |