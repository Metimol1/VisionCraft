# Available Models

You can **retrieve** a **list of available models** for image generation using the VisionCraft API.

## Request Method and URL

```
GET https://visioncraft.top/sd/models-sd3
```

## Response

The response is a JSON array containing the names of the available models, as shown below:

```
["SD3-Medium", "SD3-Anime", ...]
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to fetch the list of available models for Stable Diffusion (SD):

```python
import aiohttp
import asyncio

async def fetch_sd_models():
    """Get all available models for SD"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/sd/models-sd3') as response:
            return await response.json()

async def main():
    sd_models = await fetch_sd_models()
    print(sd_models)

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to fetch the list of available models:

```javascript
const fetch = require('node-fetch');

async function fetchSDModels() {
    const response = await fetch('https://visioncraft.top/sd/models-sd3');
    const data = await response.json();
    console.log(data);
}

fetchSDModels();
```

### cURL

Here is an example using cURL to fetch the list of available models:

```sh
curl -X GET "https://visioncraft.top/sd/models-sd3"
```
