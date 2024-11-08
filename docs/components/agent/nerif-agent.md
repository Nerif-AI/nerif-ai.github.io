---
sidebar_position: 1
---

# Nerif Agent

## Agent Class

### SimpleChatAgent

A simple agent class for the Nerif project.
This class implements a simple chat agent for the Nerif project.
It uses OpenAI's GPT models to generate responses to user inputs.

Attributes:

- `proxy_url (str)`: The URL of the proxy server for API requests.
- `api_key (str)`: The API key for authentication.
- `model (str)`: The name of the GPT model to use.
- `default_prompt (str)`: The default system prompt for the chat.
- `temperature (float)`: The temperature setting for response generation.
- `counter (NerifTokenCounter)`: Token counter instance.
- `messages (List[Any])`: The conversation history.
- `max_tokens (int)`: The maximum number of tokens to generate in the response.

Methods:

- `reset(prompt=None)`: Resets the conversation history.
- `set_max_tokens(max_tokens=None|int)`: Sets the maximum tokens limit.
- `chat(message, append=False, max_tokens=None|int)`: Sends a message and gets a response.

Example:

```python
import nerif

agent = nerif.agent.SimpleChatAgent()

print(agent.chat("What is the capital of the moon?"))
print(agent.chat("What is the capital of the moon?", max_tokens=10))
```

### SimpleEmbeddingAgent

A simple agent class for embedding text in the Nerif project.
This class provides text embedding functionality using OpenAI's embedding models.
It converts text strings into numerical vector representations.

Attributes:

- `proxy_url (str)`: The URL of the proxy server for API requests.
- `api_key (str)`: The API key for authentication.
- `model (str)`: The name of the embedding model to use.
- `counter (NerifTokenCounter)`: Optional counter for tracking token usage.

Methods:

- `encode(string: str) -> List[float]`: Encodes a string into an embedding vector.

Example:

```python
import nerif

embedding_agent = nerif.agent.SimpleEmbeddingAgent()
print(embedding_agent.encode("What is the capital of the moon?"))

```

### LogitsAgent
A simple agent for fetching logits from a model. This class provides functionality to get logit probabilities along with model responses.

Attributes:

- `proxy_url (str)`: The URL of the proxy server for API requests.
- `api_key (str)`: The API key for authentication.
- `model (str)`: The name of the model to use.
- `default_prompt (str)`: The default system prompt for the chat.
- `temperature (float)`: The temperature setting for response generation.
- `counter (NerifTokenCounter)`: Token counter instance.
- `messages (List[Any])`: The conversation history.
- `max_tokens (int)`: The maximum number of tokens to generate in the response.

Methods:

- `reset()`: Resets the conversation history.
- `set_max_tokens(max_tokens: None|int)`: Sets the maximum tokens limit.
- `chat(message: str, max_tokens: None|int, logprobs: bool = True, top_logprobs: int = 5) -> Any`: 
    Sends a message and gets a response with logits. The logprobs parameter enables logit probabilities, 
    and top_logprobs controls how many top probabilities to return.

Example:

```python
import nerif

logits_agent = nerif.agent.LogitsAgent()
print(logits_agent.chat("What is the capital of the moon?"))
```

### VisionAgent
A simple agent for vision tasks in the Nerif project.
This class implements a vision-capable agent that can process both text and images.
It uses OpenAI's GPT-4 Vision models to generate responses to user inputs that include images.

Attributes:

- `proxy_url (str)`: The URL of the proxy server for API requests.
- `api_key (str)`: The API key for authentication.
- `model (str)`: The name of the GPT model to use.
- `default_prompt (str)`: The default system prompt for the chat.
- `temperature (float)`: The temperature setting for response generation.
- `counter (NerifTokenCounter)`: Token counter instance.
- `max_tokens (int)`: Maximum tokens to generate in responses.

Methods:

- `append_message(message_type, content)`: Adds an image or text message to the conversation.
- `reset()`: Resets the conversation history.
- `set_max_tokens(max_tokens)`: Sets the maximum response token length.
- `chat(input: List[Any], append: bool, max_tokens: int|None) -> str`: Processes the input and returns a response.

Example:

```python
from nerif.agent import MessageType, VisionAgent

if __name__ == "__main__":
    vision_model = VisionAgent(model="openrouter/openai/gpt-4o-2024-08-06")
    vision_model.append_message(
        MessageType.IMAGE_URL,
        "https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png",
    )
    vision_model.append_message(MessageType.TEXT, "what is in this image?")
    response = vision_model.chat()
    print(response)
```