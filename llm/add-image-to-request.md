# Add image to request

You can use **LLaVA model** for **interacting with** your **image**.

Only **LLaVA model** support images!

## Python example

```python
from openai import OpenAI

client = OpenAI(
    api_key="your_key",
    base_url="https://visioncraft.top/v1"
)

with open("image.png", "rb") as image_file:
    base64_image = base64.b64encode(image_file.read()).decode('utf-8')

chat_completion = client.chat.completions.create(
    stream=False, # Can be True
    model="llava-1.5-7b-hf",
    messages=[
        {
        "role": "user",
        "content": [{
            "type": "text",
            "text": "What’s in this image?"
            },
            {
            "type": "image_url",
            "image_url": {
                "url": f"data:image/jpeg;base64,{base64_image}"
                }}]
        }],
)
print(chat_completion)
```