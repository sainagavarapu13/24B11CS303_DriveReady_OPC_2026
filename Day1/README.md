# Sweet Crumbs Bakery Chatbot

## Project Overview
This project implements an AI-powered chatbot for **Sweet Crumbs Home Bakery**. The chatbot helps customers get information about bakery products, prices, available options, and ordering requirements through natural-language conversations.

## Task Description
Build a simple customer-support chatbot using an LLM through the Groq API. The chatbot should understand customer questions and provide helpful responses based on the bakery information supplied in its instructions.

## Features
- Answers questions about bakery products and prices.
- Provides information about eggless options.
- Explains ordering requirements.
- Responds in a friendly and conversational manner.
- Supports customer queries in English and Telugu.
- Avoids making up information when the answer is unavailable.

## Bakery Information

| Product | Price |
|---|---:|
| Plum Cake | ₹500 |
| Chocolate Cake | ₹650 |
| Cupcake | ₹80 |

Additional rules:
- Eggless versions are available.
- Orders require 24 hours' advance notice.
- Delivery time should not be promised without confirmation.
- Unknown information should be referred to the bakery owner.

## Technologies Used
- Python
- Google Colab
- Groq API
- OpenAI Python SDK
- LLM: `openai/gpt-oss-20b`

## Implementation
1. Install the OpenAI Python SDK.
2. Configure the Groq API key securely using Google Colab Secrets.
3. Create an API client using the Groq base URL.
4. Provide the bakery information and chatbot instructions.
5. Send customer messages to the language model.
6. Display the generated responses to the customer.

## Setup and Execution

Install the required library:

```python
!pip install -q openai
```

Configure the API client:

```python
from google.colab import userdata
from openai import OpenAI

client = OpenAI(
    api_key=userdata.get("GROQ_API_KEY"),
    base_url="https://api.groq.com/openai/v1"
)
```

Add your Groq API key to Google Colab Secrets with the name `GROQ_API_KEY`, then execute the chatbot code.

## Example Queries
- What cakes are available?
- What is the price of a chocolate cake?
- Do you have eggless cakes?
- How early should I place an order?
- Can you provide information in Telugu?

## Expected Outcome
A working bakery chatbot that understands customer queries and provides accurate, friendly responses using the available bakery information.

## Project Status
Completed as part of **AI Agents Workshop – Level 1 Fundamentals, Day 1**.
