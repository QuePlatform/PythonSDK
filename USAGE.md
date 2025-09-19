<!-- Start SDK Example Usage [usage] -->
```python
# Synchronous Example
import os
from que_media import Que


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as que:

    res = que.verify_asset(asset={
        "bucket": "que-assets-dev",
        "key": "uploads/photo.jpg",
    }, mode="summary", allow_remote_manifests=False, allow_insecure_remote_http=False, include_certificates=True, limits={
        "max_asset_size_bytes": 104857600,
        "max_output_size_bytes": 104857600,
        "max_stream_copy_bytes": 104857600,
        "stream_timeout_ms": 30000,
    })

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.
```python
# Asynchronous Example
import asyncio
import os
from que_media import Que

async def main():

    async with Que(
        api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
    ) as que:

        res = await que.verify_asset_async(asset={
            "bucket": "que-assets-dev",
            "key": "uploads/photo.jpg",
        }, mode="summary", allow_remote_manifests=False, allow_insecure_remote_http=False, include_certificates=True, limits={
            "max_asset_size_bytes": 104857600,
            "max_output_size_bytes": 104857600,
            "max_stream_copy_bytes": 104857600,
            "stream_timeout_ms": 30000,
        })

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->