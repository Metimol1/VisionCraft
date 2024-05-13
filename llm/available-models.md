# Available Models

You can **retrieve** a **list of available models** for **text** generation.

## Request method and URL

```
GET https://visioncraft.top/models-llm
```

## Response

```python
["lzlv_70b_fp16_hf", "CodeLlama-34b-Instruct-hf", ...]
```

## Python example

```python
import aiohttp
import asyncio

async def fetch_LLM_models():
    """Get all available LLM models"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/models-llm') as response:
            return await response.json()

async def main():
    LLM_models = await fetch_LLM_models()
    print(LLM_models )

if __name__ == '__main__':
    asyncio.run(main())
```
