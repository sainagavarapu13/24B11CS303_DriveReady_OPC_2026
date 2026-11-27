# Day 5 – Memory and RAG in AI Agents

## Project Overview
This project is part of the **AI Agents Workshop – Level 2 (Single Agent)**. The objective is to improve the Sweet Crumbs Home Bakery AI assistant by adding conversation memory and Retrieval-Augmented Generation (RAG).

The agent can remember individual customer conversations, search bakery policies using ChromaDB, and answer questions based on stored information without making up facts.

## Objectives
- Understand the three types of memory in AI agents.
- Implement conversation memory using `InMemorySaver` and `thread_id`.
- Understand embeddings and semantic search.
- Store business information in ChromaDB.
- Implement RAG (Retrieval-Augmented Generation).
- Create a custom `search_faq` tool.
- Integrate memory and RAG into the Day 4 agent.
- Test the agent with different customers and unsupported questions.

## Technologies Used
- Python
- LangChain
- LangGraph
- LangChain-Groq
- Groq LLM
- ChromaDB
- Google Colab

## Features

### 1. Conversation Memory
Implemented conversation memory using LangGraph's `InMemorySaver` and `thread_id`.

Each customer gets a separate conversation thread, allowing the agent to remember previous messages without mixing customer conversations.

### 2. Business Knowledge Storage
Created a collection in ChromaDB to store bakery policies and FAQs.

The knowledge base includes:
- Delivery policies
- Payment methods
- Cancellation rules
- Photo cake requirements
- Order notice period
- Eggless cake availability
- Allergens information
- Cake storage instructions
- Cake messages and candles
- Discounts and pickup timings

### 3. Embeddings and Semantic Search
Used ChromaDB to convert stored information into embeddings and retrieve relevant facts based on the meaning of a customer's question.

This allows the agent to understand questions even when customers use different words.

### 4. RAG Implementation
Implemented Retrieval-Augmented Generation using the following process:

1. **Retrieve:** Search ChromaDB for relevant information.
2. **Augment:** Provide the retrieved facts to the AI agent.
3. **Generate:** Generate an answer using the retrieved information.

### 5. Custom FAQ Search Tool
Created a `search_faq` tool using LangChain's `@tool` decorator.

It searches the bakery's stored policies and returns relevant information to the agent.

### 6. Complete Single Agent
Integrated the Day 4 tools with the new memory and RAG functionality.

The agent uses:
- `get_price` – Checks product prices.
- `is_open` – Checks opening hours.
- `log_order` – Saves customer orders.
- `search_faq` – Retrieves bakery policies.

## Project Workflow

1. Customer sends a message.
2. The agent identifies the customer's request.
3. Conversation memory retrieves the relevant chat history using `thread_id`.
4. The agent selects the appropriate tool.
5. ChromaDB retrieves relevant business information for policy questions.
6. The agent generates an answer using the retrieved facts.
7. If information is unavailable, the agent responds that it will check with the owner.
8. The agent maintains separate conversations for different customers.

## Setup and Execution

### Step 1: Install Dependencies

```python
!pip install -q langchain langchain-groq chromadb
```

### Step 2: Configure Groq API Key

Store your API key in Google Colab Secrets using the name `GROQ_API_KEY`.

```python
import os
from google.colab import userdata

os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
```

### Step 3: Create the ChromaDB Collection

```python
import chromadb

client = chromadb.Client()

faq = client.get_or_create_collection(
    name="sweet_crumbs_faq"
)
```

### Step 4: Store Business Facts

Load the bakery's FAQ information into the ChromaDB collection using unique IDs and documents.

```python
faq.upsert(
    ids=list(FAQS.keys()),
    documents=list(FAQS.values())
)

print(faq.count(), "facts stored")
```

### Step 5: Create the Search Tool

Create the `search_faq` function to retrieve relevant information from ChromaDB.

### Step 6: Add Memory to the Agent

Use `InMemorySaver()` as the checkpointer and assign a separate `thread_id` to each customer.

### Step 7: Run and Test the Agent

Test the agent with different customer questions and follow-ups.

## Testing

The following test cases are used to evaluate the agent:

| Test Case | Expected Behaviour |
|---|---|
| Do you deliver? | Retrieve delivery policy |
| Is the plum cake nut-free? | Explain allergen information |
| How much notice for a photo cake? | Return 48 hours |
| Can I pay by UPI? | Explain payment policy |
| Do you sell biryani? | Avoid guessing and check with the owner |
| What is my name? | Remember information from the same thread |
| Switch customer thread | Keep customer conversations separate |

The existing `run_tests()` function and `tests.csv` from Day 3 are used to evaluate the agent.

**Target:** Achieve at least 80% test pass rate.

## Learning Outcomes

By completing Day 5, I learned how to:
- Implement short-term conversation memory.
- Manage multiple customer conversations using thread IDs.
- Understand embeddings and semantic search.
- Store and retrieve information using ChromaDB.
- Implement RAG in an AI agent.
- Create custom retrieval tools using LangChain.
- Reduce hallucinations by grounding answers in business information.
- Integrate tools, memory, knowledge and testing into one AI agent.

## Conclusion

Day 5 completes the Level 2 Single Agent project by combining tools, conversation memory and RAG. The Sweet Crumbs Home Bakery assistant can now manage customer conversations, retrieve business policies, answer questions using stored information and handle unsupported questions without making assumptions.

**Workshop:** AI Agents Workshop  
**Level:** Level 2 – Single Agent  
**Day:** 5 – Memory and RAG  
**Platform:** Google Colab  
**Case Study:** Sweet Crumbs Home Bakery
