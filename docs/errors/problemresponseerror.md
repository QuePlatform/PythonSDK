# ProblemResponseError

An RFC 7807 problem details response.


## Fields

| Field                                                    | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `type`                                                   | *str*                                                    | :heavy_check_mark:                                       | N/A                                                      | about:blank                                              |
| `title`                                                  | *str*                                                    | :heavy_check_mark:                                       | N/A                                                      | rate_limited                                             |
| `status`                                                 | *int*                                                    | :heavy_check_mark:                                       | N/A                                                      | 429                                                      |
| `code`                                                   | *str*                                                    | :heavy_check_mark:                                       | N/A                                                      | rate_limited                                             |
| `detail`                                                 | *OptionalNullable[str]*                                  | :heavy_minus_sign:                                       | N/A                                                      | try again in 5000 ms                                     |
| `details`                                                | [OptionalNullable[models.Details]](../models/details.md) | :heavy_minus_sign:                                       | N/A                                                      | {<br/>"try_again_in_ms": 5000<br/>}                      |