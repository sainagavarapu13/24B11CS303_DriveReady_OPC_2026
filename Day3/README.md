# Day 3 – Sweet Crumbs AI Assistant Using LangChain

## Project Overview 

Build an AI-powered customer support assistant for Sweet Crumbs Home Bakery using LangChain and the Groq API.

The assistant answers customer questions using predefined bakery information, remembers previous conversations, follows business rules, and handles customer queries in English or Telugu.

## Technologies Used

- Python
- Google Colab
- LangChain
- LangChain Groq
- Groq API
- ChatPromptTemplate
- MessagesPlaceholder
- StrOutputParser
- CSV

## Implementation

### 1. Environment Setup

Install the required packages and configure the Groq API key using Google Colab Secrets.

Initialize the ChatGroq model with the required temperature setting.

### 2. Create the System Prompt

Define a detailed system prompt for Sweet Crumbs Home Bakery.

The prompt contains:

- Bakery information and available products.
- Product prices and eggless options.
- Order requirements and advance notice.
- Delivery and payment restrictions.
- Customization guidelines.
- Cancellation and refund limitations.
- Customer communication rules.
- Response language and word limit.

### 3. Implement Prompt Templates

Use LangChain's `ChatPromptTemplate` to organize messages.

Use `MessagesPlaceholder` to insert previous conversation messages dynamically.

The prompt contains three parts:
- System message: Defines the assistant's behaviour.
- History: Contains previous user and assistant messages.
- Human message: Contains the current customer question.

### 4. Build the LCEL Chain

Create a processing pipeline using LangChain Expression Language (LCEL).

```python
chain = prompt | llm | StrOutputParser()
```

The pipeline:
1. Receives the formatted prompt.
2. Sends it to the language model.
3. Converts the model response into a string.

### 5. Implement Conversation Memory

Create a `history` list to store customer and assistant messages.

Implement an `ask()` function that:
- Accepts a customer question.
- Passes previous conversation history to the chain.
- Generates an answer.
- Stores both the question and answer for future interactions.

### 6. Perform Automated Chatbot Testing

Use a CSV file containing customer questions and expected keywords.

Implement `run_tests()` to:
- Read test cases using Python's CSV module.
- Send each question to the chatbot.
- Compare the response with the expected keyword.
- Display PASS or FAIL.
- Calculate the overall test success percentage.

**Testing result:** 15 out of 20 test cases passed, achieving a 75% pass rate.

### 7. Introduction to LangChain Agents

Create a basic LangChain agent using `create_agent()`.

```python
agent_order = create_agent(
    model=llm,
    tools=[],
    system_prompt=SYSTEM
)
```

Test the agent with a bakery-related question.

This is an introductory implementation with an empty tool list. Real tool integration is planned for a later session.

## Additional Testing

The chatbot was tested with customer scenarios involving:

- Birthday cake customization.
- Astronomy-themed cake designs.
- Eggless cake availability.
- Advance-order requirements.
- Customer allergy concerns.
- Birthday cake messages.
- Delivery and pickup questions.
- Payment methods.
- Cake transportation and storage.
- Remembering previous conversation details.

## Final Outcome

Successfully implemented:

1. A bakery customer support assistant using LangChain.
2. Dynamic prompt templates with conversation history.
3. An LCEL processing chain.
4. Session-based conversational memory.
5. Automated CSV-based chatbot testing.
6. Test result reporting with PASS/FAIL status.
7. An introductory LangChain agent.

**Day 3 Deliverable:** A conversational bakery assistant with memory, automated testing, and a basic introduction to LangChain agents.
