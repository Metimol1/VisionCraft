# Available Loras

You can **retrieve** a **list of available loras** for image generation.

## Request method and URL

```
GET https://visioncraft.top/sd/loras-sd
```

## Response

```python
["AddMoreDetails-DetailEnhancerTweakerLoRA-AddMoreDetails", "yuzudetail-rendering-colorful-unrealfeel", ...]
```

## Python example

```python
import aiohttp
import asyncio

async def fetch_sd_loras():
    """Get all available loras for SD"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/sd/loras-sd') as response:
            return await response.json()

async def main():
    sd_loras = await fetch_sd_loras()
    print(sd_loras)

if __name__ == '__main__':
    asyncio.run(main())
```