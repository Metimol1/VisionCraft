# VisionCraft API Documentation

## Introduction

The VisionCraft API documentation is designed for users who wish to interact with the API for image generation. This documentation will provide you with a comprehensive overview of the functionality and usage guidelines of the API.

## Functional testing

If you want to try how well my API generates images, then go to the [official site](https://rohkife.domcloud.io). There you can try all the models available in the API.

## Obtaining an API Key

To start using the VisionCraft API, you need to obtain an API key. This key is essential for every request to the API. You can obtain the key by following these steps:

1. **Subscribe to the [VisionCraft Telegram channel](https://t.me/visioncraft_channel).**

   To receive an API key, users are **required** to be subscribed to this channel. If you are already subscribed, proceed to the next step.

2. **Send the `/key` command to the [VisionCraft bot](https://t.me/VisionCraft_bot).**

   After subscribing to the channel, send this command to the bot in the chat. The bot's response will contain your API key. Please save this key, as it will be used for authentication when interacting with the API. Key generation takes approximately 15 seconds.

3. **Secure your key.**

   It is essential to protect your API key. Do not share it with other users, and do not post it in public places. Otherwise, your key will be banned, and generating a new key is not possible. One Telegram account is associated with one key.

## Interacting with the API

Once you have obtained your API key, you are ready to interact with the VisionCraft API. Below are the primary capabilities of the API.

### Available Models

You can retrieve a list of available models for image generation. Each model has its unique characteristics and generation style.

#### Request:
```
GET https://rohkife.domcloud.io/models
```

#### Response:
```
["3Guofeng3", "absolutereality", "absolutereality_v181", "amIReal", "analog-diffusion-1.0", ...]
```

### Image Generation

After selecting a specific model, you can generate images using the API. To do this, you need to make a POST request and provide the necessary parameters.

#### Request:
```
POST https://rohkife.domcloud.io/generate
```

#### Request Parameters:
- `model` (string) - the name of the chosen model
- `prompt` (string) - a text prompt for generation
- `image_count` (integer) - the number of images to generate (up to 5 in a single request)
- `token` (string) - your API key

#### Request Example:
```
{
  "model": "absolutereality",
  "prompt": "Beautiful landscape",
  "image_count": 3,
  "token": "your_api_key"
}
```

The response to this request will contain a list of generated images in base64 format.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://rohkife.domcloud.io"

# Obtain your API key
api_key = "your_api_key"

# Get a list of available models
models = requests.get(f"{api_url}/models")
print(models.json())

# Generate images using a specific model
model = "absolutereality"
prompt = "Beautiful landscape"
image_count = 3

data = {
    "model": model,
    "prompt": prompt,
    "image_count": image_count,
    "token": api_key
}

response = requests.post(f"{api_url}/generate", json=data)
images = response.json()
for i, image in enumerate(images):
    with open(f"generated_image_{i}.png", "wb") as f:
        f.write(base64.b64decode(image))
```

**JavaScript Example:**

```
// JavaScript code for interacting with VisionCraft API
const fetch = require('node-fetch');

// Define the API endpoint
const apiUrl = "https://rohkife.domcloud.io";

// Obtain your API key
const apiKey = "your_api_key";

// Get a list of available models
fetch(`${apiUrl}/models`)
  .then(response => response.json())
  .then(models => console.log(models));

// Generate images using a specific model
const model = "absolutereality";
const prompt = "Beautiful landscape";
const imageCount = 3;

const data = {
  model: model,
  prompt: prompt,
  image_count: imageCount,
  token: apiKey
};

fetch(`${apiUrl}/generate`, {
  method: 'POST',
  body: JSON.stringify(data),
  headers: {
    'Content-Type': 'application/json'
  }
})
  .then(response => response.json())
  .then(images => {
    images.forEach((image, i) => {
      // Save the base64 image data to a file or use it as needed
    });
  });
```

## Key Limitations

It's important to note that your API key is linked to your subscription to the VisionCraft Telegram channel. If you unsubscribe from the channel, your key will cease to function. However, when you resubscribe to the channel, the key automatically renews its functionality.

## Contact Information

If you have any questions or requests, feel free to reach out to us. We are always ready to assist you. For communication, use my [Telegram](https://t.me/metimol).

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Metim0l/VisionCraft&type=Timeline)](https://star-history.com/#Metim0l/VisionCraft&Timeline)