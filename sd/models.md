# Available Models

You can **retrieve** a **list of available models** for image generation.

## Request method and URL

```
GET https://visioncraft.top/sd/models-sd
```

## Response

```python
["Dalcefo-v5", "AnythingV5NoVAE-Ink-noVAE", ...]
```

## Python example

```python
import aiohttp
import asyncio

async def fetch_sd_models():
    """Get all available models for SD"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/sd/models-sd') as response:
            return await response.json()

async def main():
    sd_models = await fetch_sd_models()
    print(sd_models)

if __name__ == '__main__':
    asyncio.run(main())
```
