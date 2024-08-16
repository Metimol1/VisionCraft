# Available Samplers

You can **retrieve** a **list of available samplers** for image generation using the VisionCraft API.

## Request Method and URL

```
GET https://visioncraft.top/sd/samplers
```

## Response

The response is a JSON array containing the names of the available samplers, as shown below:

```
["Euler a", "Euler", "LMS", ...]
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to fetch the list of available samplers for Stable Diffusion (SD):

```python
import aiohttp
import asyncio

async def fetch_sd_samplers():
    """Get all available samplers for SD models"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/sd/samplers') as response:
            return await response.json()

async def main():
    sd_samplers = await fetch_sd_samplers()
    print(sd_samplers)

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to fetch the list of available samplers:

```javascript
const fetch = require('node-fetch');

async function fetchSDSamplers() {
    const response = await fetch('https://visioncraft.top/sd/samplers');
    const data = await response.json();
    console.log(data);
}

fetchSDSamplers();
```

### cURL

Here is an example using cURL to fetch the list of available samplers:

```sh
curl -X GET "https://visioncraft.top/sd/samplers"
```
