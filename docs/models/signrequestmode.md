# ~~SignRequestMode~~

The signing mode to use.
* `server_measure`: The server will download the asset, calculate its hash, and embed the manifest. Requires `manifest_json`.
* `client_hash`: The client provides the asset hash directly. (Not yet implemented).


> :warning: **DEPRECATED**: This will be removed in a future release, please migrate away from it as soon as possible.


## Values

| Name             | Value            |
| ---------------- | ---------------- |
| `SERVER_MEASURE` | server_measure   |
| `CLIENT_HASH`    | client_hash      |