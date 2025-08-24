# TrustListResponse

The C2PA trust list bundle, containing trusted certificate authorities and manufacturers.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `version`                                                            | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  | dev-1                                                                |
| `issued_at`                                                          | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | N/A                                                                  | 2025-08-15T20:00:00Z                                                 |
| `data`                                                               | [models.Data](../models/data.md)                                     | :heavy_check_mark:                                                   | N/A                                                                  |                                                                      |