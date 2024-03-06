# VisionCraft API Documentation

## Official links:
- [Telegram channel](https://t.me/visioncraft_channel)
- [Android app](https://play.google.com/store/apps/details?id=com.karlmathuthu.vision_craft_mobile)
- [Flutter package](https://pub.dev/packages/flutter_vision_craft)

## Table of Contents
- [Introduction](#introduction)
- [Obtaining an API Key](#obtaining-an-api-key)
- [Limits](#limits)
- [Interacting with the API](#interacting-with-the-api)
  - [Image Generation with Stable Diffusion 1.x](#image-generation)
    - [Available Models](#available-models)
    - [Available Samplers](#available-samplers)
    - [Available Loras](#available-loras)
    - [Image generation](#image-generation)
  - [Image generation with Stable Diffusion XL](#stable-diffusion-xl)
    - [Available Models](#available-xl-models)
    - [Available Samplers](#available-xl-samplers)
    - [Available Schedulers](#available-xl-schedulers)
    - [Image generation](#generate-image-xl)
  - [Midjourney](#midjourney)
    - [Generate image](#midjourney-generate-image)
    - [Get image](#midjourney-get-image)
  - [Openjourney](#openjourney)
  - [Image to Image generation](#image-to-image)
    - [Available Schedulers](#available-img2img-schedulers)
    - [Available Refiners](#available-img2img-refiners)
  - [LLM](#llm-generation)
    - [Available LLM models](#available-llm-models)
    - [Text generation](#text-generation)
    - [Image to Text](#image-to-text)
  - [Text to GIF generation](#text-to-gif)
  - [Image to Video generation](#image-to-video)
  - [Upscale Image](#upscale-image)
  - [Whisper](#whisper)
- [Key Limitations](#key-limitations)
- [Contact Information](#contact-information)

## Introduction

The VisionCraft API documentation is designed for users who wish to interact with the API for image generation. This documentation will provide you with a comprehensive overview of the functionality and usage guidelines of the API.

## Obtaining an API Key

To start using the VisionCraft API, you need to obtain an API key. This key is essential for every request to the API. You can obtain the key by following these steps:

1. **Subscribe to the [VisionCraft Telegram channel](https://t.me/visioncraft_channel).**

   To receive an API key, users are **required** to be subscribed to this channel. If you are already subscribed, proceed to the next step.

2. **Send the `/key` command to the [VisionCraft bot](https://t.me/VisionCraft_bot).**

   After subscribing to the channel, send this command to the bot in the chat. The bot's response will contain your API key. Please save this key, as it will be used for authentication when interacting with the API. Key generation takes approximately 15 seconds.

3. **Secure your key.**

   It is essential to protect your API key. Do not share it with other users, and do not post it in public places. Otherwise, your key will be banned, and generating a new key is not possible. One Telegram account is associated with one key.

## Limits

API has FREE users and PREMIUM users. PREMIUM subscription cost $10, and with premium subscription users don't have any limits. But free users have limits with some models. You can look limits for free users here:

https://api.visioncraft.top/limits

If a model is not listed on this page, it means it is unlimited for free users.

# Interacting with the API

## Image Generation

### Available Models

You can retrieve a list of available models for image generation. Each model has its unique characteristics and generation style.

#### Request:
```
GET https://api.visioncraft.top/models
```

#### Response:
```
["3guofeng3_v3.4", "absolutereality_v1.6", "absolutereality_v1.8.1", "amIReal_v4.1", "analog_diffusion_v1", "anything_v3.0", "anything_v4.5", "anything_V5", ...]
```

### Available Samplers

You can retrieve a list of available samplers for image generation.

#### Request:
```
GET https://api.visioncraft.top/samplers
```

#### Response:
```
["Euler", "Euler a", "LMS", "Heun", "DPM2", "DPM2 a", ...]
```

### Available Loras

You can retrieve a list of available Loras for image generation.

#### Request:
```
GET https://api.visioncraft.top/loras
```

#### Response:
```
["0mib3_v10", "3DMM_V12", "age_slider_v20", "arcane_offset", "AstralMecha", "epi_noiseoffset2", "eye_size_slider_v1", ...]
```


After selecting a specific model, you can generate images using the API. To do this, you need to make a POST request and provide the necessary parameters.

### Stable Diffusion

#### Request:
```
POST https://api.visioncraft.top/generate
```

#### Request Parameters:
- `model` (string) - the name of the chosen model
- `sampler` (string) - the name of the chosen sampler
- `prompt` (string) - a text prompt for generation
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `image_count` (integer) - the number of images to generate (up to 5 in a single request)
- `token` (string) - your API key
- `cfg_scale` (integer) (optional: default is 10) - the CFG Scale (0-20)
- `steps` (integer) (optional: default is 30)- the number of steps (1-50)
- `loras` (dict) (optional) - a dictionary in which the key is the name Lora, and the meaning is its weight.

**About parameters**

**CFG_Scale**: How strongly the image should conform to the text - lower values produce more creative results.

**Steps**: How many times to improve the generated image iteratively; higher values take longer; very low values can produce bad results.

**Loras**: LoRA models are small trained models for Stable Diffusion that make additional changes to image generation and are used in conjunction with standard models.

#### Request Example:
```
{
  "model": "anything_V5",
  "sampler": "Euler",
  "prompt": "Beautiful landscape",
  "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
  "image_count": 3,
  "token": "your_api_key",
  "cfg_scale": 8,
  "steps": 30,
  "loras": {"3DMM_V12": 1, "GrayClay_V1.5.5": 2}
}
```

The response to this request will contain a list of links to the generated images.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

# Generate images using a specific model
model = "anything_V5"
sampler = "Euler"
image_count = 3
cfg_scale = 8
steps = 30
loras = {"3DMM_V12": 1, "GrayClay_V1.5.5": 2}

# Set up the data to send in the request
data = {
    "model": model,
    "sampler": sampler,
    "prompt": "Beautiful landscape",
    "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)),((extra limbs)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render",
    "image_count": image_count,
    "token": api_key,
    "cfg_scale": cfg_scale,
    "steps": steps,
    "loras": loras
}

# Send the request to generate images
response = requests.post(f"{api_url}/generate", json=data, verify=True)

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


## Stable Diffusion XL

### Available XL Models

You can retrieve a list of available models for image generation XL. Each model has its unique characteristics and generation style.

#### Request:
```
GET https://api.visioncraft.top/models-xl
```

#### Response:
```
["sdxl-base","sdxl-turbo", ...]
```

### Available XL Samplers

You can retrieve a list of available samplers for image generation.

#### Request:
```
GET https://api.visioncraft.top/samplers-xl
```

#### Response:
```
["euler","euler_ancestral","heun","heunpp2","dpm_2","dpm_2_ancestral","Ims", ...]
```

### Available XL Schedulers

You can retrieve a list of available schedulers for image generation.

#### Request:
```
GET https://api.visioncraft.top/schedulers-xl
```

#### Response:
```
["normal","karras","exponential","sgm_uniform", ...]
```

After selecting a specific model, sampler and scheduler you can generate images using the API. To do this, you need to make a POST request and provide the necessary parameters.


### Generate image XL

#### Request:
```
POST https://api.visioncraft.top/generate-xl
```

#### Request Parameters:
- `prompt` (string) - a text prompt for generation
- `model` (string) - one of the available SDXL models.
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `token` (string) - your API key
- `height` (integer) - generated image height (minimum 512, maximum 1024), default is 1024
- `width` (integer) - generated image width (minimum 512, maximum 1024), default is 1024
- `sampler` (string) - one of the available SDXL samplers.
- `scheduler` (string) - one of the available SDXL schedulers.

#### Request Example:
```
{
  "prompt": "Beautiful landscape",
  "model": "sdxl-turbo",
  "negative_prompt": "bad quality",
  "token": "your_api_key",
  "height": 1024,
  "width": 1024,
  "sampler": "euler",
  "scheduler": "normal"
}
```

The response to this request will contain a your image.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

# Set up the data to send in the request
data = {
    "prompt": "Beautiful landscape",
    "model": "sdxl-turbo",
    "negative_prompt": "bad quality",
    "token": api_key,
    "width": 1024,
    "height": 1024,
    "sampler": "euler",
    "scheduler": "normal"
}

# Send the request to generate images
response = requests.post(f"{api_url}/generate-xl", json=data)

# Get the image from the response
image = response.content

# Save the image locally
with open(f"generated_image.png", "wb") as f:
    f.write(image)
```

## Midjourney

### Midjourney generate image

#### Request:
```
POST https://api.visioncraft.top/midjourney
```

#### Request Parameters:
- `prompt` (string) - a text prompt for generation
- `token` (string) - your API key from VisionCraft API.

#### Request Example:
```
{
  "prompt": "Paper cut of a seascape, with serene colors, delicate waves, Alex Garant, Edison bulb, calming blue background --ar 9:16 --v 5.2",
  "token": "your_api_key"
}
```

#### Response:
```
{
  "statusCode": 200,
  "message": "Success",
  "data": "your_request_id"
}
```

### Midjourney get image
#### Request:
```
POST https://api.visioncraft.top/midjourney/result
```

#### Request Parameters:
- `task_id` (string) - parameter `data` from your image generation request.
- `token` (string) - your API key from VisionCraft API.

#### Request Example:
```
{
  "task_id": "75435",
  "token": "your_api_key"
}
```

#### Response:
If your image is still being generated, you will receive a response like this:
```
{
  "ImageID": 75435,
  "Status": "generating"
}
```

If your image is already ready, you will receive this response:
```
{
  "ImageID": 75435,
  "Status": "success",
  "StartTime": "2024-02-25T09:15:02.000Z",
  "RequestTime": "2024-02-25T09:13:48.000Z",
  "FinishTime": "2024-02-25T09:20:54.000Z",
  "URL": "Your image URL"
}
```

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

# Set up the data to send in the request
data = {
    "prompt": "Paper cut of a seascape, with serene colors, delicate waves, Alex Garant, Edison bulb, calming blue background --ar 9:16 --v 5.2",
    "token": api_key
}

# Send the request to generate images
response = requests.post(f"{api_url}/midjourney", json=data)

if "data" in response.json():
    image_id = response.json()["data"]
    data_image = {
        "task_id": str(image_id),
        "token": api_key
    }
    
    while True:
        response = requests.post(f"{api_url}/midjourney/result", json=data_image)
        if "URL" in response.json():
            image = response.json()["URL"]
            break
    
    image_data = requests.get(image)
    
    # Save generated image
    with open(f"generated_image.png", "wb") as f:
        f.write(image_data.content)
else:
    print(response.json())
```

## Openjourney

Openjourney is an open source Stable Diffusion fine tuned model on Midjourney images, by PromptHero.

Include `mdjrny-v4 style` in prompt. Here you'll find hundreds of [Openjourney prompts](https://prompthero.com/openjourney-prompts?utm_source=huggingface&utm_medium=referral)

#### Request:
```
POST https://api.visioncraft.top/openjourney
```

#### Request Parameters:
- `prompt` (string) - a text prompt for generation
- `token` (string) - your API key from VisionCraft API.
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `cfg_scale` (float) (optional: default is 7.5) - the CFG Scale (1-20)
- `steps` (integer) (optional: default is 50)- the number of steps (1-50)
- `height` (integer) - generated image height (minimum 128, maximum 1024), default is 1024
- `width` (integer) - generated image width (minimum 128, maximum 1024), default is 1024


#### Request Example:
```
{
  "token": "your_token",
  "prompt": "Magical girl, mystical watercolor painting, stars, , flow, watercolor ultra resolution, Soft Lighting, Intricate, Pastel colors, Digital painting, Artstation, Dreamlike, Whimsical, art by loish and sakimichan and mandy jurgens",
  "negative_prompt": "Ugly, Disfigured, Deformed, Low quality, Pixelated, Blurry, Grains, Text, Watermark, Signature, Out of frame, Disproportioned, Bad proportions, Gross proportions, Bad anatomy, Duplicate, Cropped, Extra hands, Extra arms, Extra legs, Extra fingers, Extra limbs, Long neck, Mutation, Mutilated, Mutated hands, Poorly drawn face, Poorly drawn hands, Missing hands, Missing arms, Missing legs, Missing fingers, Low resolution, Morbid.",
  "steps": 50,
  "cfg_scale": 7.5,
  "height": 1024,
  "width": 1024
}
```

The response should be contain bytecode from your image.

> [!IMPORTANT]
> Height and Width must be one of [128, 256, 384, 448, 512, 576, 640, 704, 768, 832, 896, 960, 1024]


**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

# Set up the data to send in the request
data = {
    "token": api_key,
    "prompt": "Magical girl, mystical watercolor painting, stars, , flow, watercolor ultra resolution, Soft Lighting, Intricate, Pastel colors, Digital painting, Artstation, Dreamlike, Whimsical, art by loish and sakimichan and mandy jurgens",
    "negative_prompt": "Ugly, Disfigured, Deformed, Low quality, Pixelated, Blurry, Grains, Text, Watermark, Signature, Out of frame, Disproportioned, Bad proportions, Gross proportions, Bad anatomy, Duplicate, Cropped, Extra hands, Extra arms, Extra legs, Extra fingers, Extra limbs, Long neck, Mutation, Mutilated, Mutated hands, Poorly drawn face, Poorly drawn hands, Missing hands, Missing arms, Missing legs, Missing fingers, Low resolution, Morbid.",
    "steps": 50,
    "cfg_scale": 7.5,
    "height": 1024,
    "width": 1024
}

# Send the request to generate images
response = requests.post(f"{api_url}/openjourney", json=data)

# Extract the image from the response
image = response.content

# Save the image locally
with open(f"generated_image.png", "wb") as f:
    f.write(image)
```


## Image to Image

### Available Img2img Schedulers

You can retrieve a list of available Schedulers for image to image generation.

#### Request:
```
GET https://api.visioncraft.top/img2img/schedulers
```

#### Response:
```
["DDIM", "DPMSolverMultistep", "HeunDiscrete", "KarrasDPM", ...]
```

### Available Img2img Refiners

You can retrieve a list of available Refiners for image to image generation.

#### Request:
```
GET https://api.visioncraft.top/img2img/refiners
```

#### Response:
```
["no_refiner", "expert_ensemble_refiner", "base_image_refiner", ...]
```

After selecting specific models, schedulers and refiners you can generate images.


#### Request:
```
POST https://api.visioncraft.top/img2img
```

#### Request Parameters:
- `prompt` (string) - a text prompt for generation
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `token` (string) - your API key
- `image` (string) - your image in base64 format, or URL to your image.
- `mask` (string) (optional: default is `None`) - If you want to change only a certain part of your image, and not all at once, then you can pass the base64 code of your mask to this parameter. Read [here](https://huggingface.co/docs/diffusers/main/en/using-diffusers/inpaint) what a mask should look like.
- `scheduler` (string) (optional: default is `DDIM`) - one of the available img2img schedulers
- `steps` (integer) (optional: default is 50) - the number of steps (1-50)
- `strength` (float) (optional: default is 0.8) - Prompt strength. 1.0 corresponds to full destruction of information in image.
- `refiner` (string) (optional: default is `no_refiner`) - one of the available img2img refiners

#### Request Example:
```
{
  "prompt": "Beautiful lady",
  "negative_prompt": "bad quality",
  "token": "your_api_key",
  "image": "your_image_in_base64_format or url_to_your_image",
  "steps": 50,
  "strength": 0.8,
  "refiner": "no_refiner",
  "scheduler": "DDIM"
}
```

The response to this request will contain a bytecode of the generated image.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests, base64

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

with open("my_image.png", "rb") as image:
  image_base64 = base64.b64encode(image.read()).decode("utf-8")

# Set up the data to send in the request
data = {
    "prompt": "Beautiful girl",
    "negative_prompt": "bad quality",
    "token": api_key,
    "image": image_base64,
    "steps": 50,
    "strength": 0.8,
    "refiner": "no_refiner",
    "scheduler": "DDIM"
}

# Send the request to generate images
response = requests.post(f"{api_url}/img2img", json=data)

# Extract the image from the response
image = response.content

# Save the image locally
with open(f"generated_image.png", "wb") as f:
    f.write(image)
```


## LLM Generation

### Available LLM Models

You can retrieve a list of available models for text generation.

#### Request:
```
GET https://api.visioncraft.top/models-llm
```

#### Response:
```
["Mixtral-8x7B-Instruct-v0.1", "CodeLlama-70b-Instruct-hf", ...]
```

### Text generation
After selecting model, you can generate text.

#### Request:
```
POST https://api.visioncraft.top/llm
```

#### Request Parameters:
- `model` (string) - the name of the chosen LLM model
- `token` (string) - your API key
- `messages` (list) - messages to the LLM

#### Request Example:
```
{
  "model": "gpt-3.5-turbo",
  "token": "your_api_key",
  "messages": [
    {"role": "user", "content": "What is the meaning of life?"}
  ]
}
```

The response to this request will contain a response from LLM model.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests, json

response = requests.post(
  url="https://api.visioncraft.top/llm",
  data=json.dumps({
    "token": "your_token",
    "model": "gpt-3.5-turbo",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Tell me a joke."},
      {"role": "assistant", "content": "Sure, here's a joke: Why don't scientists trust atoms? Because they make up everything!"},
      {"role": "user", "content": "That's a good one! Tell me another."},
      {"role": "assistant", "content": "Why did the computer go to therapy? It had too many bytes of emotional baggage."},
      {"role": "user", "content": "Haha, nice! What's the weather like today?"}
    ]
  })
)

print(response.json())
```

### Image to Text
You can use LLaVA model for interacting with your image.

#### Request:
```
POST https://api.visioncraft.top/llm
```

#### Request Example:
```
{
  "model": "llava-1.5-7b-hf",
  "token": "your_api_key",
  "messages": [
    {"role": "user", "content": "What is on this image?", "image": "your_image_in_base64_or_url_format"}
  ]
}
```

The response to this request will contain a response from LLM model.

**Python Example:**

```
import requests, json, base64

with open("my_image.png", "rb") as i:
    image = i.read()
image = base64.b64encode(image).decode("utf-8")

response = requests.post(
  url="https://api.visioncraft.top/llm",
  data=json.dumps({
    "token": "your_api_key",
    "model": "llava-1.5-7b-hf",
    "messages": [
      {"role": "user", "content": "What is it?", "image": image}
    ]
  })
)

print(response.json())
```


## Text to GIF

#### Request:
```
POST https://api.visioncraft.top/generate-gif
```

#### Request Parameters:
- `token` (string) - your API key
- `sampler` (string) - the name of the chosen sampler
- `prompt` (string) - a text prompt for generation
- `negative_prompt` (string) (optional) - text prompt that the model should not be drawn on the picture.
- `cfg_scale` (integer) (optional: default is 10) - the CFG Scale (0-20)
- `steps` (integer) (optional: default is 30)- the number of steps (1-50)

#### Request Example:
```
{
  "sampler": "Euler",
  "prompt": "Beautiful landscape",
  "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)), ((extra limbs)), ((close up)), ((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), ((ugly)), (((bad proportions))), (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, tiling, poorly drawn feet, body out of frame",
  "token": "your_api_key",
  "cfg_scale": 8,
  "steps": 30
}
```

The response to this request will contain a list of link to the generated GIF.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

# Generate images using a specific model
sampler = "Euler"
cfg_scale = 8
steps = 30

# Set up the data to send in the request
data = {
    "sampler": sampler,
    "prompt": "Beautiful landscape",
    "negative_prompt": "canvas frame, cartoon, 3d, ((disfigured)), ((bad art)), ((deformed)),((extra limbs)),((close up)),((b&w)), weird colors, blurry, (((duplicate))), ((morbid)), ((mutilated)), [out of frame], extra fingers, mutated hands, ((poorly drawn hands)), ((poorly drawn face)), (((mutation))), (((deformed))), ((ugly)), blurry, ((bad anatomy)), (((bad proportions))), ((extra limbs)), cloned face, (((disfigured))), out of frame, ugly, extra limbs, (bad anatomy), gross proportions, (malformed limbs), ((missing arms)), ((missing legs)), (((extra arms))), (((extra legs))), mutated hands, (fused fingers), (too many fingers), (((long neck))), Photoshop, video game, ugly, tiling, poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, body out of frame, blurry, bad art, bad anatomy, 3d render",
    "token": api_key,
    "cfg_scale": cfg_scale,
    "steps": steps
}

# Send the request to generate images
response = requests.post(f"{api_url}/generate-gif", json=data, verify=True)

# Extract the image URLs from the response
image_urls = response.json()["images"]

# Download and save the generated images
for i, image_url in enumerate(image_urls):
    # Get the image data from the URL
    response = requests.get(image_url)
    # Save the image locally
    with open(f"generated_image_{i}.gif", "wb") as f:
        f.write(response.content)
```

## Image to Video

#### Request:
```
POST https://api.visioncraft.top/img2video
```

#### Request Parameters:
- `token` (string) - your API key
- `image` (string) - your image in base64 format or URL to your image

#### Request Example:
```
{
  "token": "your_api_key",
  "image": "your_image_in_base64_format or url_to_your_image"
}
```

The response to this request will contain a generated image.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests, base64

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

with open("my_image.png", "rb") as image:
  image_base64 = base64.b64encode(image.read()).decode("utf-8")

# Set up the data to send in the request
data = {
    "token": api_key,
    "image": image_base64,
}

# Send the request to generate images
response = requests.post(f"{api_url}/img2video", json=data)

# Get the result
result = response.content

# Save the video locally
with open(f"generated_video.mp4", "wb") as f:
    f.write(result)
```


## Upscale Image

#### Request:
```
POST https://api.visioncraft.top/upscale
```

#### Request Parameters:
- `token` (string) - your API key
- `image` (string) - your image in base64 format or URL to your image.

#### Request Example:
```
{
  "token": "your_api_key",
  "image": "your_image_in_base64 or url_to_your_image"
}
```

The response to this request will contain a list of links to the generated images.

**Python Example:**

```
import requests, base64

def upscale_request(image):
    b = base64.b64encode(image).decode('utf-8')
    payload = {
        "token": "your_token",
        "image": b
    }
    url = 'https://api.visioncraft.top/upscale'
    headers = {"content-type": "application/json"}

    resp = requests.post(url, json=payload, headers=headers)
    content = resp.content
    return content

image = open('my_image.png', 'rb').read()
upscaled_image = upscale_request(image)
with open('upscaled_image.png', 'wb') as f:
    f.write(upscaled_image)
```

## Whisper

#### Request:
```
POST https://api.visioncraft.top/whisper
```

#### Request Parameters:
- `token` (string) - your API key
- `audio` (string) - your audio in base64 format or URL to your audio

#### Request Example:
```
{
  "token": "your_api_key",
  "audio": "your_audio_in_base64_format or url_to_your_audio"
}
```

The response to this request will contain a JSON with transcribed text from your audio.

**Python Example:**

```
# Python code for interacting with VisionCraft API
import requests, base64

# Define the API endpoint
api_url = "https://api.visioncraft.top"

# Obtain your API key
api_key = "your_api_key"

with open("my_audio.mp3", "rb") as audio:
  audio_base64 = base64.b64encode(audio.read()).decode("utf-8")

# Set up the data to send in the request
data = {
    "token": api_key,
    "audio": audio_base64,
}

# Send the request to generate images
response = requests.post(f"{api_url}/whisper", json=data)

# Get the result
result = response.json()

# Print the result
print(result)
```

## Key Limitations

It's important to note that your API key is linked to your subscription to the VisionCraft Telegram channel. If you unsubscribe from the channel, your key will cease to function. However, when you resubscribe to the channel, the key automatically renews its functionality.

## Contact Information

If you have any questions or requests, feel free to reach out to us. We are always ready to assist you. For communication, use my [Telegram](https://t.me/metimol).
