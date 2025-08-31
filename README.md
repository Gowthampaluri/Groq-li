Groq Python API library
PyPI version

The Groq Python library provides convenient access to the Groq REST API from any Python 3.8+ application. The library includes type definitions for all request params and response fields, and offers both synchronous and asynchronous clients powered by httpx.

It is generated with Stainless.

Documentation
The REST API documentation can be found on console.groq.com. The full API of this library can be found in api.md.

Installation
# install from PyPI
pip install groq

Usage
The full API of this library can be found in api.md.

import os
from groq import Groq

client = Groq(
    api_key=os.environ.get("GROQ_API_KEY"),  # This is the default and can be omitted
)

chat_completion = client.chat.completions.create(
    messages=[
        {
            "role": "user",
            "content": "Explain the importance of low latency LLMs",
        }
    ],
    model="llama3-8b-8192",
)
print(chat_completion.choices[0].message.content)

While you can provide an api_key keyword argument, we recommend using python-dotenv to add GROQ_API_KEY="My API Key" to your .env file so that your API Key is not stored in source control.
