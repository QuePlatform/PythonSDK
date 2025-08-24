<!-- Start SDK Example Usage [usage] -->
```python
# Synchronous Example
import os
from que import Que, models


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as q_client:

    res = q_client.verify_asset(asset={
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
from que import Que, models

async def main():

    async with Que(
        api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
    ) as q_client:

        res = await q_client.verify_asset_async(asset={
            "url": "https://example.com/images/provenance-image.jpg",
        }, mode=models.VerifyRequestMode.DETAILED)

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->