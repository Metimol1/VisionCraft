# Text Generation

After **selecting a model**, you can **generate text** using the VisionCraft API.

## Request Method and URL

```
POST https://visioncraft.top/v1/chat/completions
```

## Parameters

| Parameter          | Type    | Description                                                                                               |
|--------------------|---------|-----------------------------------------------------------------------------------------------------------|
| `model`*           | string  | The name of the chosen LLM model                                                                          |
| `max_tokens`       | integer | Maximum length of the generated text (min: `128`, max: `100000`, default: `512`)                          |
| `temperature`      | float   | Sampling temperature. 0 means deterministic output, values >1 encourage diversity (min: `0`, max: `100`, default: `0.7`)  |
| `top_p`            | float   | Probability threshold for token sampling (min: `0`, max: `1`, default: `0.9`)                             |
| `top_k`            | integer | Number of top tokens to sample from (min: `0`, max: `99999`, default: `0`)                                |
| `repetition_penalty`| float   | Penalty for token repetition (min: `0.01`, max: `5`, default: `1`)                                        |
| `presence_penalty` | float   | Positive values penalize new tokens based on their presence in the text so far (min: `-2`, max: `2`, default: `0`) |
| `frequency_penalty`| float   | Positive values penalize new tokens based on their frequency in the text so far (min: `-2`, max: `2`, default: `0`) |
| `messages`*        | list    | Messages to the LLM                                                                                       |

<sup>* Required parameters</sup>

## Request Example

### Request Headers

```
Authorization: Bearer your_api_key
```

### Request Body

```
{
  "model": "Mixtral-8x7B-Instruct-v0.1",
  "messages": [
    {
      "role": "user",
      "content": 'There are 50 books in a library. Sam decides to read 5 of the books. How many books are there now? If there are 45 books, say "1". Else, if there is the same amount of books, say "2".'
    }
  ]
}
```

## Examples

### Python

Here is a Python example using the `openai` library to generate text:

```python
from openai import OpenAI

client = OpenAI(
    api_key="your_api_key",
    base_url="https://visioncraft.top/v1"
)

chat_completion = client.chat.completions.create(
    stream=False, # Can be True
    model="Mixtral-8x7B-Instruct-v0.1",
    messages=[
        {
            "role": "user",
            "content": 'There are 50 books in a library. Sam decides to read 5 of the books. How many books are there now? If there are 45 books, say "1". Else, if there is the same amount of books, say "2".'
        },
    ],
)
print(chat_completion)
```

### JavaScript (Node.js)

Here is a JavaScript example using the `node-fetch` library to generate text:

```javascript
const fetch = require('node-fetch');

async function generateText() {
    const response = await fetch('https://visioncraft.top/v1/chat/completions', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer your_api_key'
        },
        body: JSON.stringify({
            model: "Mixtral-8x7B-Instruct-v0.1",
            messages: [
                {
                    role: "user",
                    content: 'There are 50 books in a library. Sam decides to read 5 of the books. How many books are there now? If there are 45 books, say "1". Else, if there is the same amount of books, say "2".'
                }
            ]
        })
    });
    const data = await response.json();
    console.log(data);
}

generateText();
```

### cURL

Here is an example using cURL to generate text:

```sh
curl -X POST "https://visioncraft.top/v1/chat/completions" \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer your_api_key" \
     -d '{
            "model": "Mixtral-8x7B-Instruct-v0.1",
            "messages": [
                {
                    "role": "user",
                    "content": "There are 50 books in a library. Sam decides to read 5 of the books. How many books are there now? If there are 45 books, say \"1\". Else, if there is the same amount of books, say \"2\"."
                }
            ]
        }'
```