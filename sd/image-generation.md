# Image Generation

After **selecting** a specific **model and sampler** you can **generate images using** the **API**. To do this, you need to make a **POST reque**st and provide the **necessary parameters**.

## Request method and URL

```
POST https://visioncraft.top/sd
```

## Parameters (<mark style="color:red;">\*</mark> required)

<table><thead><tr><th width="178">Parameter</th><th width="91">Type</th><th>Description</th></tr></thead><tbody><tr><td>token<mark style="color:red;">*</mark></td><td>string</td><td>Your API key</td></tr><tr><td>model<mark style="color:red;">*</mark></td><td>string</td><td>One of the available SD model</td></tr><tr><td>prompt<mark style="color:red;">*</mark></td><td>string</td><td>A text prompt for generation</td></tr><tr><td>negative_prompt</td><td>string</td><td>Text prompt that the model shouldn't be drawn on the picture</td></tr><tr><td>sampler<mark style="color:red;">*</mark></td><td>string</td><td>One of the available SD sampler</td></tr><tr><td>steps<mark style="color:red;">*</mark></td><td>integer</td><td>How many times to improve the generated image iteratively; higher values take longer; very low values can produce bad results <strong>(min: </strong><mark style="color:red;"><strong>1</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>30</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>30</strong></mark><strong>)</strong></td></tr><tr><td>width<mark style="color:red;">*</mark></td><td>integer</td><td>Generated image width <strong>(min: </strong><mark style="color:red;"><strong>64</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>1024</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>1024</strong></mark><strong>)</strong></td></tr><tr><td>height<mark style="color:red;">*</mark></td><td>integer</td><td>Generated image height <strong>(min: </strong><mark style="color:red;"><strong>64</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>1024</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>1024</strong></mark><strong>)</strong></td></tr><tr><td>cfg_scale</td><td>integer</td><td>How strongly the image should conform to the text <strong>(min: </strong><mark style="color:red;"><strong>1</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>30</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>7</strong></mark><strong>)</strong></td></tr><tr><td>loras</td><td>dict</td><td>Dictionary of available <a href="broken-reference">loras</a> <strong>(max </strong><mark style="color:red;"><strong>5</strong></mark><strong> in dict)</strong></td></tr></tbody></table>

## Request example

```javascript
{
  "model": "sdxl-base",
  "prompt": "Beautiful landscape",
  "negative_prompt": "bad quality",
  "token": "your_api_key",
  "sampler": "Euler",
  "steps": 30,
  "width": 1024,
  "height": 1024,
  "cfg_scale": 7,
  "loras": {}
}
```

## Loras usage

```javascript
{
  "lora_name_1": priority,
  "lora_name_2": priority,
  "lora_name_3": priority,
}
```

## Python example

```python
import aiohttp
import asyncio

async def generate_image(api_url, data) -> bytes:
    async with aiohttp.ClientSession() as session:
        async with session.post(f"{api_url}/sd", json=data) as response:
            image = await response.read()
            return image

async def main():
    # Define the API endpoint
    api_url = "https://visioncraft.top"
    # Obtain your API key
    api_key = "your_api_key"

    # Generate image
    prompt = "Beautiful landscape"
    model = "sdxl-base"
    
    # Set up the data to send in the request
    data = {
        "model": model,
        "prompt": prompt,
        "token": api_key,
    }
    
    # Generate image asynchronously
    image = await generate_image(api_url, data)
    # Save the image locally
    with open(f"generated_image.png", "wb") as f:
        f.write(image)

if __name__ == "__main__":
    asyncio.run(main())
```