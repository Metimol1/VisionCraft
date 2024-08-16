# Available Loras

You can **retrieve** a **list of available loras** for image generation using the VisionCraft API.

## Request Method and URL

```
GET https://visioncraft.top/image/loras/sd
```

## Response

The response is a JSON array containing the names of the available loras, as shown below:

```
["AddMoreDetails-DetailEnhancerTweakerLoRA-AddMoreDetails", "yuzudetail-rendering-colorful-unrealfeel", ...]
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to fetch the list of available loras for Stable Diffusion (SD):

```python
import aiohttp
import asyncio

async def fetch_sd_loras():
    """Get all available loras for SD"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/image/loras/sd') as response:
            return await response.json()

async def main():
    sd_loras = await fetch_sd_loras()
    print(sd_loras)

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to fetch the list of available loras:

```javascript
const fetch = require('node-fetch');

async function fetchSDLoras() {
    const response = await fetch('https://visioncraft.top/image/loras/sd');
    const data = await response.json();
    console.log(data);
}

fetchSDLoras();
```

### cURL

Here is an example using cURL to fetch the list of available loras:

```sh
curl -X GET "https://visioncraft.top/image/loras/sd"
```
