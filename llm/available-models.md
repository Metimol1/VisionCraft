# Available Models

You can **retrieve** a **list of available models** for **text generation** using the VisionCraft API.

## Request Method and URL

```
GET https://visioncraft.top/models-llm
```

## Response

The response is a JSON array containing the names of the available models, as shown below:

```
["lzlv_70b_fp16_hf", "CodeLlama-34b-Instruct-hf", ...]
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to fetch the list of available models for text generation (LLM):

```python
import aiohttp
import asyncio

async def fetch_llm_models():
    """Get all available LLM models"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/models-llm') as response:
            return await response.json()

async def main():
    llm_models = await fetch_llm_models()
    print(llm_models)

if __name__ == '__main__':
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to fetch the list of available models:

```javascript
const fetch = require('node-fetch');

async function fetchLLMModels() {
    const response = await fetch('https://visioncraft.top/models-llm');
    const data = await response.json();
    console.log(data);
}

fetchLLMModels();
```

### cURL

Here is an example using cURL to fetch the list of available models:

```sh
curl -X GET "https://visioncraft.top/models-llm"
```