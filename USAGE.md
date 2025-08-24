<!-- Start SDK Example Usage [usage] -->
```python
# Synchronous Example
import os
from que_media import Que, models


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as que:

    res = que.verify_asset(asset={
        "url": "https://example.com/images/provenance-image.jpg",
    }, mode=models.VerifyRequestMode.DETAILED)

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.
```python
# Asynchronous Example
import asyncio
import os
from que_media import Que, models

async def main():

    async with Que(
        api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
    ) as que:

        res = await que.verify_asset_async(asset={
            "url": "https://example.com/images/provenance-image.jpg",
        }, mode=models.VerifyRequestMode.DETAILED)

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->