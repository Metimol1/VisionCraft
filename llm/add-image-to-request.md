# Add Image to Request

You can use the **LLaVA model** for **interacting with** your **image**. Only the **LLaVA model** supports images!

## Examples

### Python

Here is a Python example using the `openai` library to interact with an image:

```python
import base64
from openai import OpenAI

client = OpenAI(
    api_key="your_key",
    base_url="https://visioncraft.top/v1"
)

# Read and encode the image
with open("image.png", "rb") as image_file:
    base64_image = base64.b64encode(image_file.read()).decode('utf-8')

# Create a chat completion request with the image
chat_completion = client.chat.completions.create(
    stream=False, # Can be True
    model="llava-1.5-7b-hf",
    messages=[
        {
            "role": "user",
            "content": [
                {"type": "text", "text": "What’s in this image?"},
                {"type": "image_url", "image_url": {"url": f"data:image/jpeg;base64,{base64_image}"}}
            ]
        }
    ],
)
print(chat_completion)
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to interact with an image:

```javascript
const fetch = require('node-fetch');
const fs = require('fs');

async function generateTextWithImage() {
    const imageBuffer = fs.readFileSync('image.png');
    const base64Image = imageBuffer.toString('base64');

    const response = await fetch('https://visioncraft.top/v1/chat/completions', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            model: "llava-1.5-7b-hf",
            token: "your_api_key",
            messages: [
                {
                    role: "user",
                    content: [
                        { type: "text", text: "What’s in this image?" },
                        { type: "image_url", image_url: { url: `data:image/jpeg;base64,${base64Image}` } }
                    ]
                }
            ]
        })
    });
    
    const data = await response.json();
    console.log(data);
}

generateTextWithImage();
```

### cURL

Here is an example using cURL to interact with an image:

```sh
# Encode the image to base64
base64_image=$(base64 -w 0 image.png)

# Make the request
curl -X POST "https://visioncraft.top/v1/chat/completions" \
     -H "Content-Type: application/json" \
     -d '{
            "model": "llava-1.5-7b-hf",
            "token": "your_api_key",
            "messages": [
                {
                    "role": "user",
                    "content": [
                        { "type": "text", "text": "What’s in this image?" },
                        { "type": "image_url", "image_url": { "url": "data:image/jpeg;base64,'"$base64_image"'" } }
                    ]
                }
            ]
         }'
```