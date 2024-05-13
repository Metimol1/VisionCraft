# Text Generation

After **selecting model**, you can **generate text**.

## Request method and URL

```
POST https://visioncraft.top/v1/chat/completions
```

## Parameters (<mark style="color:red;">\*</mark> required)

<table><thead><tr><th width="189">Parameter</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td>model<mark style="color:red;">*</mark></td><td>string</td><td>The name of the chosen LLM model</td></tr><tr><td>token<mark style="color:red;">*</mark></td><td>string</td><td>Your API key</td></tr><tr><td>max_tokens</td><td>integer</td><td>Maximum length of the newly generated generated text <strong>(min: </strong><mark style="color:red;"><strong>128</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>100000</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>512</strong></mark><strong>)</strong></td></tr><tr><td>temperature</td><td>float</td><td>Temperature to use for sampling. 0 means the output is deterministic, values greater than 1 encourage more diversity <strong>(min: </strong><mark style="color:red;"><strong>0</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>100</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>0.7</strong></mark><strong>)</strong></td></tr><tr><td>top_p</td><td>float</td><td>Sample from the set of tokens with highest probability such that sum of probabilies is higher than p. Lower values focus on the most probable tokens. Higher values sample more low-probability tokens <strong>(min: </strong><mark style="color:red;"><strong>0</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>1</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>0.9</strong></mark><strong>)</strong></td></tr><tr><td>top_k</td><td>float</td><td>Sample from the best k (number of) tokens. 0 means off <strong>(min: </strong><mark style="color:red;"><strong>0</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>99999</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>0</strong></mark><strong>)</strong></td></tr><tr><td>repetition_penalty</td><td>float</td><td>Value of 1 means no penalty, values greater than 1 discourage repetition, smaller than 1 encourage repetition <strong>(min: </strong><mark style="color:red;"><strong>0.01</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>5</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>1</strong></mark><strong>)</strong></td></tr><tr><td>presence_penalty</td><td>float</td><td>Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics <strong>(min: </strong><mark style="color:red;"><strong>-2</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>2</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>0</strong></mark><strong>)</strong></td></tr><tr><td>frequency_penalty</td><td>float</td><td>Positive values penalize new tokens based on how many times they appear in the text so far, increasing the model's likelihood to talk about new topics <strong>(min: </strong><mark style="color:red;"><strong>-2</strong></mark><strong>, max: </strong><mark style="color:red;"><strong>2</strong></mark><strong>, default: </strong><mark style="color:red;"><strong>0</strong></mark><strong>)</strong></td></tr><tr><td>messages<mark style="color:red;">*</mark></td><td>list</td><td>Messages to the LLM</td></tr></tbody></table>

## Python example

```python
from openai import OpenAI

client = OpenAI(
    api_key="your_key",
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