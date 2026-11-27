
# Day 4 – AI Agent with Tools, Pydantic & Google Sheets

## Project Overview
This project is part of the **AI Agents Workshop – Level 2 (Single Agent)**. It builds a customer-support and order-management agent for **Sweet Crumbs Home Bakery** using LangChain and Groq.

The agent can answer customer questions, check cake prices, verify bakery opening hours, and save confirmed customer orders directly to Google Sheets.

## Objectives
- Understand how AI agents use tools and function calling.
- Create custom tools using LangChain's `@tool` decorator.
- Build an AI agent using `create_agent`.
- Handle API errors and rate limits.
- Extract structured information using Pydantic.
- Connect Google Sheets using `gspread`.
- Validate and save customer orders automatically.

## Technologies Used
- Python
- LangChain
- LangChain-Groq
- Groq LLM
- Pydantic
- Google Colab
- Google Sheets
- gspread

## Features

### 1. Price Checking
The `get_price` tool checks the bakery menu and calculates the total price based on the selected item and quantity.

### 2. Opening Hours
The `is_open` tool checks the bakery's opening hours for a particular day.

### 3. Order Validation
A Pydantic `Order` model validates customer information, including:
- Customer name
- Cake item
- Quantity
- Pickup date
- Eggless preference

It also checks that the quantity is at least one and that the item belongs to the supported menu.

### 4. Google Sheets Integration
The `log_order` tool saves confirmed orders to a Google Sheet.

Each order is stored as a separate row containing the customer details and calculated total amount.

### 5. AI Agent
The LangChain agent uses the available tools to understand customer requests and perform the required actions.

It asks for missing order details instead of saving incomplete orders.

### 6. Error Handling
The project uses `try-except` blocks to handle errors and provide polite responses when the agent encounters a problem.

## Project Workflow

1. Customer sends a message.
2. The AI agent understands the request.
3. The agent selects the appropriate tool.
4. The tool checks the information or processes the order.
5. Pydantic validates the order details.
6. The confirmed order is saved to Google Sheets.
7. The agent provides a confirmation to the customer.

## Setup and Execution

### Step 1: Install Dependencies

```python
!pip install -q langchain langchain-groq gspread
```

### Step 2: Configure Groq API Key

Store your API key in Google Colab Secrets with the name `GROQ_API_KEY`.

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

### Step 3: Configure Google Sheets

Authenticate your Google account in Colab and connect using `gspread`.

```python
from google.colab import auth
auth.authenticate_user()

import gspread
from google.auth import default

creds, _ = default()
gc = gspread.authorize(creds)
```

### Step 4: Run the Agent

Execute the notebook cells in order to initialize the model, tools, Google Sheet, and agent.

### Step 5: Test the Agent

Try the following customer messages:

- "Are you open on Sunday?"
- "How much are 2 chocolate cakes?"
- "I'm Sai. Please book 2 eggless chocolate cakes for 24 Dec."
- "Do you sell donuts?"
- "I want to order 2 plum cakes."

Check the Google Sheet to verify that valid orders are saved correctly.

## Expected Output

The agent should:
- Return accurate prices using the `get_price` tool.
- Provide opening hours using the `is_open` tool.
- Ask for missing details before saving an order.
- Reject invalid menu items and quantities.
- Save valid orders to Google Sheets.
- Confirm the order details and total amount.

## Learning Outcomes

By completing Day 4, I learned how to:
- Connect an LLM with Python tools.
- Understand the function-calling process.
- Build a single AI agent using LangChain.
- Validate structured data using Pydantic.
- Integrate Google Sheets with an AI application.
- Handle errors and prevent incomplete or invalid orders.

## Conclusion

Day 4 demonstrates how an AI agent can move beyond generating text and perform practical business tasks. By combining LangChain tools, Pydantic validation, and Google Sheets, the Sweet Crumbs assistant can handle customer queries and automate order management.

**Workshop:** AI Agents Workshop  
**Level:** Level 2 – Single Agent  
**Day:** 4 – Tools, Structured Output and Google Sheets  
**Platform:** Google Colab
