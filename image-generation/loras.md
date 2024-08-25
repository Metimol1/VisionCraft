# Available Loras

You can retrieve lists of available Loras for different models or categories using the VisionCraft API.

## Request Method and URL

To get the list of Loras for a specific model or category, use the following GET request:

```
GET https://visioncraft.top/image/loras/{category}
```

Replace `{category}` with one of the following options:

- SD-3.0
- SD-2.0
- SD-1.4
- HunYuanDiT
- SD-1.5
- Pony
- Kolors
- FLUX.1
- SDXL-1.0
- HunYuanDiT-v1.2

## Response

The response is expected to be a JSON array containing the names of the available Loras for the specified category.

## Examples

### Python

Here's a Python example using the `aiohttp` library to fetch the list of available Loras for a specific category:

```python
import aiohttp
import asyncio

async def fetch_loras(category):
    """Get available Loras for a specific category"""
    url = f'https://visioncraft.top/image/loras/{category}'
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def main():
    categories = ['SD-3.0', 'SDXL-1.0', 'HunYuanDiT']
    for category in categories:
        loras = await fetch_loras(category)
        print(f"{category} Loras:")
        print(loras)
        print()

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here's a JavaScript example using the `node-fetch` library to fetch the list of available Loras for a specific category:

```javascript
const fetch = require('node-fetch');

async function fetchLoras(category) {
    const response = await fetch(`https://visioncraft.top/image/loras/${category}`);
    const data = await response.json();
    console.log(`${category} Loras:`);
    console.log(data);
    console.log();
}

async function main() {
    const categories = ['SD-3.0', 'SDXL-1.0', 'HunYuanDiT'];
    for (const category of categories) {
        await fetchLoras(category);
    }
}

main();
```

### cURL

Here's an example using cURL to fetch the list of available Loras for a specific category:

```sh
curl -X GET "https://visioncraft.top/image/loras/SD-3.0"
```

Replace `SD-3.0` with any of the other categories to get Loras for different models or types.