# Available Samplers

You can **retrieve** a **list of available sanplers** for image generation.

## Request method and URL

```
GET https://visioncraft.top/sd/samplers
```

## Response

```python
["Euler a", "Euler", "LMS", ...]
```

## Python example

```python
import aiohttp
import asyncio

async def fetch_sd_samplers():
    """Get all available loras for SD models"""
    async with aiohttp.ClientSession() as session:
        async with session.get('https://visioncraft.top/sd/samplers') as response:
            return await response.json()

async def main():
    sd_samplers = await fetch_sd_samplers()
    print(sd_samplers)

if __name__ == '__main__':
    asyncio.run(main())
```