# Image Generation

You can **generate images using** the **API**. To do this, you need to make a **POST reque**st and provide the **necessary parameters**.

## Request method and URL

```
POST https://visioncraft.top/kandinsky
```

## Parameters (<mark style="color:red;">\*</mark> required)

<table><thead><tr><th width="178">Parameter</th><th width="91">Type</th><th>Description</th></tr></thead><tbody><tr><td>token<mark style="color:red;">*</mark></td><td>string</td><td>Your API key</td></tr><tr><td>prompt<mark style="color:red;">*</mark></td><td>string</td><td>A text prompt for generation</td></tr><tr><td>negative_prompt</td><td>string</td><td>Text prompt that the model shouldn't be drawn on the picture</td></tr></tbody></table>

## Request example

```javascript
{
  "token": "string",
  "prompt": "string",
  "negative_prompt": "string"
}
```

## Python example

```python
import aiohttp
import asyncio

async def generate_image(api_url, data) -> bytes:
    async with aiohttp.ClientSession() as session:
        async with session.post(f"{api_url}/kandinsky", json=data) as response:
            image = await response.read()
            return image

async def main():
    # Define the API endpoint
    api_url = "https://visioncraft.top"
    # Obtain your API key
    api_key = "your_api_key"

    # Generate image
    prompt = "Beautiful landscape"
 
    # Set up the data to send in the request
    data = {
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
