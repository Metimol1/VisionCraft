# GIF Generation

## Request method and URL

```
POST https://visioncraft.top/generate-gif
```

## Parameters (<mark style="color:red;">\*</mark> required)

<table><thead><tr><th width="174">Parameter</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>token<mark style="color:red;">*</mark></td><td>string</td><td>Your API key</td></tr><tr><td>sampler<mark style="color:red;">*</mark></td><td>string</td><td>The name of the chosen sampler</td></tr><tr><td>prompt<mark style="color:red;">*</mark></td><td>string</td><td>A text prompt for generation</td></tr><tr><td>negative_prompt</td><td>integer</td><td>Text prompt that the model shouldn't be drawn</td></tr><tr><td>cfg_scale</td><td>integer</td><td>How strongly the GIF should conform to the text - lower values produce more creative results <strong>(min: </strong><mark style="color:red;"><strong>0</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>20</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>10</strong></mark><strong>)</strong></td></tr><tr><td>steps</td><td>integer</td><td>How many times to improve the generated image iteratively; higher values take longer; very low values can produce bad results <strong>(min: </strong><mark style="color:red;"><strong>1</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>50</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>30</strong></mark><strong>)</strong></td></tr></tbody></table>

## Request example

```javascript
{
  "sampler": "Euler",
  "prompt": "Beautiful landscape",
  "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
  "token": "your_api_key",
  "cfg_scale": 8,
  "steps": 30
}
```

## Python example

```python
import aiohttp
import asyncio

async def generate_images(api_url, data):
    async with aiohttp.ClientSession() as session:
        async with session.post(f"{api_url}/generate-gif", json=data, verify_ssl=False) as response:
            return await response.json()

async def download_image(session, image_url, filename):
    async with session.get(image_url) as response:
        image_data = await response.read()
        with open(filename, "wb") as f:
            f.write(image_data)

async def main():
    # Define the API endpoint
    api_url = "https://visioncraft.top"
    # Obtain your API key
    api_key = "your_api_key"

    # Generate images using a specific model
    sampler = "Euler"
    prompt = "Beautiful landscape"
    cfg_scale = 8
    steps = 30

    # Set up the data to send in the request
    data = {
        "sampler": sampler,
        "prompt": prompt,
        "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)),((extra limbs)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render",
        "token": api_key,
        "cfg_scale": cfg_scale,
        "steps": steps
    }

    # Generate images asynchronously
    response = await generate_images(api_url, data)

    # Extract the image URLs from the response
    image_url = response["images"][0]

    async with aiohttp.ClientSession() as session:
        await download_image(session, image_url, f"generated_image.gif")

if __name__ == "__main__":
    asyncio.run(main())
```
