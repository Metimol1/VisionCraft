# VisionCraft API Documentation

## Table of Contents
- [Introduction](#introduction)
- [Functional Testing](#functional-testing)
- [Obtaining an API Key](#obtaining-an-api-key)
- [Interacting with the API](#interacting-with-the-api)
  - [Available Models](#available-models)
  - [Available Samplers](#available-samplers)
  - [Image Generation](#image-generation)
    - [Stable Diffusion 1.x](#stable-diffusion)
  - [Beta features](#beta-features)
    - [Stable Diffusion XL Turbo](#sdxl-turbo)
- [Key Limitations](#key-limitations)
- [Libraries](#libraries)
- [Contact Information](#contact-information)
- [Star History](#star-history)

## Introduction

The VisionCraft API documentation is designed for users who wish to interact with the API for image generation. This documentation will provide you with a comprehensive overview of the functionality and usage guidelines of the API.

## Functional testing

If you want to try how well my API generates images, then go to the [official site](https://visioncraft.vercel.app). There you can try all the models available in the API.

## Obtaining an API Key

To start using the VisionCraft API, you need to obtain an API key. This key is essential for every request to the API. You can obtain the key by following these steps:

1. **Subscribe to the [VisionCraft Telegram channel](https://t.me/visioncraft_channel).**

   To receive an API key, users are **required** to be subscribed to this channel. If you are already subscribed, proceed to the next step.

2. **Send the `/key` command to the [VisionCraft bot](https://t.me/VisionCraft_bot).**

   After subscribing to the channel, send this command to the bot in the chat. The bot's response will contain your API key. Please save this key, as it will be used for authentication when interacting with the API. Key generation takes approximately 15 seconds.

3. **Secure your key.**

   It is essential to protect your API key. Do not share it with other users, and do not post it in public places. Otherwise, your key will be banned, and generating a new key is not possible. One Telegram account is associated with one key.

## Interacting with the API

### Available Models

You can retrieve a list of available models for image generation. Each model has its unique characteristics and generation style.

#### Request:
```
GET https://visioncraftapi--vladalek05.repl.co/models
```

#### Response:
```
["3guofeng3_v3.4", "absolutereality_v1.6", "absolutereality_v1.8.1", "amIReal_v4.1", "analog_diffusion_v1", "anything_v3.0", "anything_v4.5", "anything_V5", ...]
```

### Available Samplers

You can retrieve a list of available samplers for image generation.

If you do not know which sampler to choose, I recommend reading [this article](https://stable-diffusion-art.com/samplers/).

#### Request:
```
GET https://visioncraftapi--vladalek05.repl.co/samplers
```

#### Response:
```
["Euler", "Euler a", "LMS", "Heun", "DPM2", "DPM2 a", ...]
```

## Image Generation

After selecting a specific model, you can generate images using the API. To do this, you need to make a POST request and provide the necessary parameters.

### Stable Diffusion

#### Request:
```
POST https://visioncraftapi--vladalek05.repl.co/generate
```

#### Request Parameters:
- `model` (string) - the name of the chosen model
- `sampler` (string) - the name of the chosen sampler
- `prompt` (string) - a text prompt for generation
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `image_count` (integer) - the number of images to generate (up to 5 in a single request)
- `token` (string) - your API key
- `cfg_scale` (integer) (optional: default is 10) - the CFG Scale (0-20, defaults to 10)
- `steps` (integer) (optional: default is 30)- the number of steps (1-30, defaults to 30)

**About parameters**

**CFG_Scale**: How strongly the image should conform to the text - lower values produce more creative results.

**Steps**: How many times to improve the generated image iteratively; higher values take longer; very low values can produce bad results.

#### Request Example:
```
{
  "model": "anything_V5",
  "sampler": "Euler",
  "prompt": "Beautiful landscape",
  "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)),((extra limbs)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render",
  "image_count": 3,
  "token": "your_api_key",
  "cfg_scale": 8,
  "steps": 30
}
```

The response to this request will contain a list of links to the generated images.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://visioncraftapi--vladalek05.repl.co"

# Obtain your API key
api_key = "your_api_key"

# Generate images using a specific model
model = "anything_V5"
sampler = "Euler"
image_count = 3
cfg_scale = 8
steps = 30

# Set up the data to send in the request
data = {
    "model": model,
    "sampler": sampler,
    "prompt": "Beautiful landscape",
    "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)),((extra limbs)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render",
    "image_count": image_count,
    "token": api_key,
    "cfg_scale": cfg_scale,
    "steps": steps
}

# Send the request to generate images
response = requests.post(f"{api_url}/generate", json=data, verify=False)

# Extract the image URLs from the response
image_urls = response.json()["images"]

# Download and save the generated images
for i, image_url in enumerate(image_urls):
    # Get the image data from the URL
    response = requests.get(image_url)
    # Save the image locally
    with open(f"generated_image_{i}.png", "wb") as f:
        f.write(response.content)
```

## Beta features
The features written below are in open testing, may occasionally stop working and may be removed or changed.

### SDXL-Turbo

#### Request:
```
POST https://visioncraftapi--vladalek05.repl.co/beta/sdxl-turbo
```

#### Request Parameters:
- `prompt` (string) - a text prompt for generation
- `image_count` (integer) - the number of images to generate (up to 5 in a single request)
- `token` (string) - your API key
- `height` (integer) - generated image height (minimum 64, maximum 1024), default is 1024
- `width` (integer) - generated image width (minimum 64, maximum 1024), default is 1024

#### Request Example:
```
{
  "prompt": "Beautiful landscape",
  "image_count": 1,
  "token": "your_api_key",
  "height: 768,
  "width": 1024
}
```

The response to this request will contain a list of links to the generated images.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://visioncraftapi--vladalek05.repl.co"

# Obtain your API key
api_key = "your_api_key"

# Set up the data to send in the request
data = {
    "prompt": "Beautiful landscape",
    "image_count": 2,
    "token": api_key,
    "width": 1024,
    "height": 768
}

# Send the request to generate images
response = requests.post(f"{api_url}/beta/sdxl-turbo", json=data, verify=False)

# Extract the image URLs from the response
image_urls = response.json()["images"]

# Download and save the generated images
for i, image_url in enumerate(image_urls):
    # Get the image data from the URL
    response = requests.get(image_url)
    # Save the image locally
    with open(f"generated_image_{i}.png", "wb") as f:
        f.write(response.content)
```

## Key Limitations

It's important to note that your API key is linked to your subscription to the VisionCraft Telegram channel. If you unsubscribe from the channel, your key will cease to function. However, when you resubscribe to the channel, the key automatically renews its functionality.

## Libraries

#### [Flutter package for using VisionCraft API](https://pub.dev/packages/flutter_vision_craft)

## Contact Information

If you have any questions or requests, feel free to reach out to us. We are always ready to assist you. For communication, use my [Telegram](https://t.me/metimol).

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Metim0l/VisionCraft&type=Timeline)](https://star-history.com/#Metim0l/VisionCraft&Timeline)