# Available Models

You can retrieve lists of available models for image generation using the VisionCraft API. The models are categorized into different types based on their architecture and capabilities.

## Request Method and URL

To get the list of models for a specific category, use the following GET request:

```
GET https://visioncraft.top/image/models/{category}
```

Replace `{category}` with one of the following options:

- SD-3.0
- SD-1.5
- SDXL-1.0
- Pony
- Kolors
- SD-2.0
- PixArt
- FLUX.1
- Playground-v2
- SD-1.4
- HunYuanDiT-v1.2

## Response

The response is a JSON array containing the names of the available models for the specified category.

## Model Categories

1. **SD-3.0**: Latest version of Stable Diffusion models
2. **SD-1.5**: Stable Diffusion 1.5 models
3. **SDXL-1.0**: Stable Diffusion XL 1.0 models
4. **Pony**: Pony Diffusion models
5. **Kolors**: Kolors models
6. **SD-2.0**: Stable Diffusion 2.0 models
7. **PixArt**: PixArt models
8. **FLUX.1**: FLUX.1 models
9. **Playground-v2**: Playground v2 models
10. **SD-1.4**: Stable Diffusion 1.4 models
11. **HunYuanDiT-v1.2**: HunYuanDiT v1.2 models

## Examples

### Python

Here's a Python example using the `aiohttp` library to fetch the list of available models for a specific category:

```python
import aiohttp
import asyncio

async def fetch_models(category):
    """Get available models for a specific category"""
    url = f'https://visioncraft.top/image/models/{category}'
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def main():
    categories = ['SD-3.0', 'SDXL-1.0', 'PixArt']
    for category in categories:
        models = await fetch_models(category)
        print(f"{category} models:")
        print(models)
        print()

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here's a JavaScript example using the `node-fetch` library to fetch the list of available models for a specific category:

```javascript
const fetch = require('node-fetch');

async function fetchModels(category) {
    const response = await fetch(`https://visioncraft.top/image/models/${category}`);
    const data = await response.json();
    console.log(`${category} models:`);
    console.log(data);
    console.log();
}

async function main() {
    const categories = ['SD-3.0', 'SDXL-1.0', 'PixArt'];
    for (const category of categories) {
        await fetchModels(category);
    }
}

main();
```

### cURL

Here's an example using cURL to fetch the list of available models for a specific category:

```sh
curl -X GET "https://visioncraft.top/image/models/SD-3.0"
```

Replace `SD-3.0` with any of the other categories to get models for different types.
