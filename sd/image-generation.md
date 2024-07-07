# Image Generation

After **selecting** a specific **model and sampler**, you can **generate images** using the **VisionCraft API**. To do this, you need to make a **POST request** and provide the **necessary parameters**.

## Request Method and URL

```
POST https://visioncraft.top/sd
```

## Parameters

| Parameter        | Type    | Description                                                                                                   |
|------------------|---------|---------------------------------------------------------------------------------------------------------------|
| `token`*         | string  | Your API key                                                                                                   |
| `model`*         | string  | One of the available SD models                                                                                 |
| `prompt`*        | string  | A text prompt for generation                                                                                   |
| `negative_prompt`| string  | Text prompt that the model shouldn't be drawn on the picture                                                   |
| `sampler`*       | string  | One of the available SD samplers                                                                               |
| `steps`*         | integer | How many times to iteratively improve the image (min: `1`, max: `30`, default: `30`)                           |
| `width`*         | integer | Generated image width (min: `64`, max: `1024`, default: `1024`)                                                |
| `height`*        | integer | Generated image height (min: `64`, max: `1024`, default: `1024`)                                               |
| `cfg_scale`      | integer | How strongly the image should conform to the text (min: `1`, max: `30`, default: `7`)                          |
| `loras`          | dict    | Dictionary of available loras (max `5` in dict)                                                                |

<sup>* Required parameters</sup>

## Request Example

### Request Body

```json
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

### Loras Usage

```
{
  "lora_name_1": priority,
  "lora_name_2": priority,
  "lora_name_3": priority
}
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to generate an image:

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
        "sampler": "Euler",
        "steps": 30,
        "width": 1024,
        "height": 1024,
        "cfg_scale": 7,
        "loras": {}
    }
    
    # Generate image asynchronously
    image = await generate_image(api_url, data)
    # Save the image locally
    with open(f"generated_image.png", "wb") as f:
        f.write(image)

if __name__ == "__main__":
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to generate an image:

```javascript
const fetch = require('node-fetch');
const fs = require('fs');

async function generateImage(apiUrl, data) {
    const response = await fetch(`${apiUrl}/sd`, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
    });
    const buffer = await response.buffer();
    return buffer;
}

async function main() {
    const apiUrl = "https://visioncraft.top";
    const apiKey = "your_api_key";
    const prompt = "Beautiful landscape";
    const model = "sdxl-base";
    
    const data = {
        "model": model,
        "prompt": prompt,
        "token": apiKey,
        "sampler": "Euler",
        "steps": 30,
        "width": 1024,
        "height": 1024,
        "cfg_scale": 7,
        "loras": {}
    };
    
    const imageBuffer = await generateImage(apiUrl, data);
    fs.writeFileSync('generated_image.png', imageBuffer);
}

main();
```

### cURL

Here is an example using cURL to generate an image:

```sh
curl -X POST "https://visioncraft.top/sd" \
     -H "Content-Type: application/json" \
     -d '{
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
        }'
```