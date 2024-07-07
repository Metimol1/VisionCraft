# GIF Generation

You can generate GIFs using the VisionCraft API.

## Request Method and URL

```
POST https://visioncraft.top/generate-gif
```

## Parameters

| Parameter        | Type    | Description                                                                                                  |
|------------------|---------|--------------------------------------------------------------------------------------------------------------|
| `token`*         | string  | Your API key                                                                                                  |
| `sampler`*       | string  | The name of the chosen sampler                                                                                |
| `prompt`*        | string  | A text prompt for generation                                                                                  |
| `negative_prompt`| string  | Text prompt that the model shouldn't be drawn                                                                 |
| `cfg_scale`      | integer | How strongly the GIF should conform to the text (min: `0`, max: `20`, default: `10`)                          |
| `steps`          | integer | How many times to iteratively improve the generated image (min: `1`, max: `50`, default: `30`)                |

<sup>* Required parameters</sup>

## Request Example

### Request Body

```json
{
  "sampler": "Euler",
  "prompt": "Beautiful landscape",
  "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
  "token": "your_api_key",
  "cfg_scale": 8,
  "steps": 30
}
```

## Examples

### Python

Here is a Python example using the `aiohttp` library to generate a GIF:

```python
import aiohttp
import asyncio

async def generate_gif(api_url, data):
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

    # Generate GIF using a specific model
    sampler = "Euler"
    prompt = "Beautiful landscape"
    cfg_scale = 8
    steps = 30

    # Set up the data to send in the request
    data = {
        "sampler": sampler,
        "prompt": prompt,
        "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
        "token": api_key,
        "cfg_scale": cfg_scale,
        "steps": steps
    }

    # Generate GIF asynchronously
    response = await generate_gif(api_url, data)

    # Extract the image URL from the response
    image_url = response["images"][0]

    async with aiohttp.ClientSession() as session:
        await download_image(session, image_url, "generated_image.gif")

if __name__ == "__main__":
    asyncio.run(main())
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to generate a GIF:

```javascript
const fetch = require('node-fetch');
const fs = require('fs');

async function generateGif() {
    const response = await fetch('https://visioncraft.top/generate-gif', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            sampler: "Euler",
            prompt: "Beautiful landscape",
            negative_prompt: "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
            token: "your_api_key",
            cfg_scale: 8,
            steps: 30
        })
    });
    
    const data = await response.json();
    const imageUrl = data.images[0];
    
    const imageResponse = await fetch(imageUrl);
    const buffer = await imageResponse.buffer();
    fs.writeFileSync('generated_image.gif', buffer);
}

generateGif();
```

### cURL

Here is an example using cURL to generate a GIF:

```sh
curl -X POST "https://visioncraft.top/generate-gif" \
     -H "Content-Type: application/json" \
     -d '{
            "sampler": "Euler",
            "prompt": "Beautiful landscape",
            "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
            "token": "your_api_key",
            "cfg_scale": 8,
            "steps": 30
        }'
```