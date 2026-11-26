# Day 2 – Stateful Sweet Crumbs Home Bakery Chatbot

## Project Overview

Build an AI-powered customer-support chatbot for Sweet Crumbs Home Bakery using Python and the Groq API.

The chatbot maintains conversation history, remembers customer details during a session, calculates product prices, and follows predefined business rules.

## Technologies Used

- Python
- Google Colab
- Groq API
- OpenAI Python SDK
- JSON
- Python Decorators
- Exception Handling

## Implementation

### 1. Secure API Key Configuration

- Retrieve the Groq or OpenAI API key from environment variables or Google Colab Secrets.
- Use `getpass` as a fallback for securely entering an API key.
- Automatically configure the API client based on the key type.
- Route Groq requests through its OpenAI-compatible endpoint.

### 2. Define the Bakery Menu

Store product names and prices using a Python dictionary.

```python
MENU = {
    "plum cake": 500,
    "chocolate cake": 650,
    "cupcake": 80
}
```

### 3. Create the System Prompt

Generate the system prompt dynamically using the bakery menu.

Define:
- Chatbot role and behaviour.
- Bakery products and prices.
- 24-hour advance-order requirement.
- Eggless cake availability.
- Rules for unknown information.
- Customer name and order memory.
- Response language and word limit.

### 4. Implement a Python Decorator

Create a `log_call` decorator to track function execution and display its arguments and returned values.

Use the decorator with the `get_price()` function.

### 5. Implement Price Calculation

Create a function that calculates the total price based on the product and quantity.

```python
@log_call
def get_price(item: str, qty: int = 1) -> int:
    """Return the total price in rupees for qty of an item on the menu."""
    return MENU[item.lower().strip()] * qty
```

### 6. Implement Conversation Memory

- Maintain conversation history using a list of dictionaries.
- Store system, user, and assistant messages.
- Use `MAX_TURNS = 8` to limit the conversation context sent to the model.
- Preserve the system prompt while trimming older messages.

### 7. Implement the Chat Function

Create a `chat()` function that:
- Accepts customer messages.
- Adds messages to conversation history.
- Sends recent conversation context to the Groq model.
- Returns the chatbot response.
- Handles API rate-limit and connection errors using `try/except`.

### 8. Create the Interactive Chat Loop

Use a `while` loop to allow customers to interact continuously.

- Accept customer messages.
- Display chatbot responses.
- Stop when the customer enters `bye`, `exit`, or `quit`.
- Handle keyboard interruptions gracefully.

## Chatbot Testing

The chatbot was tested with the following customer interactions:

| Test | Customer message | Expected behaviour |
|---|---|---|
| 1 | What is your bakery name? | Introduce the bakery |
| 2 | What cakes do you offer? | Display menu and prices |
| 3 | Do you make eggless cakes? | Confirm eggless availability |
| 4 | My name is Sai. | Remember the customer's name |
| 5 | I want two chocolate cakes. | Calculate ₹1,300 |
| 6 | Can I place an order for today? | Explain the 24-hour notice |
| 7 | What is the price of five cupcakes? | Calculate ₹400 |
| 8 | Can you help me plan a birthday surprise? | Refer unknown services to the owner |
| 9 | Bye | End the conversation politely |

## Additional Practical Tasks – Your 10%

1. **Prompt Engineering:** Remove the RULES section and test how the chatbot responds to unsupported delivery requests. Restore the rules and compare the responses.

2. **Few-Shot Prompting:** Create a simple business-message classifier using three examples and test it with five new messages.

3. **Structured JSON Output:** Ask the chatbot to return order details in JSON format containing name, item, quantity, date, and eggless preference. Parse the response using `json.loads()` with exception handling.

4. **Conversation Memory:** Change `MAX_TURNS` to 2, provide your name, continue the conversation for three turns, and check whether the chatbot remembers your name.

5. **Build Your Own Business Chatbot:** Adapt the implementation for another business using:
   - A product or service dictionary.
   - A system prompt
