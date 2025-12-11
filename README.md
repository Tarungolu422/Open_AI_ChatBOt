# LLM-OpenAI Streamlit App

## Overview

This project is a lightweight Streamlit-based chatbot powered by **OpenAI GPT-5.1**, **LangChain prompt templates**, and **LLMOps monitoring using LangSmith**.
It demonstrates how to build a clean, functional GenAI application with proper prompt flow and LLM tracking.

---

## Features

- Streamlit UI for user input
- LangChain prompt template + output parsing
- GPT-5.1 integration
- LLMOps enabled using LangSmith
- Simple & clean chain-based architecture

---

## Challenges Faced

- Import errors due to LangChain version mismatches
- Fixing module paths like `ChatOpenAI` import issues
- Handling prompt formatting errors
- Streamlit rerun behavior & input state
- Secure API key management
- Enabling LangSmith tracing correctly

---

## Installation

### 1. Clone the Repository

```
git clone <your-repo-url>
cd llm-openai-streamlit
```

### 2. Create a Virtual Environment

```
python -m venv .venv
# Windows
.\.venv\Scripts\activate
# Mac/Linux
source .venv/bin/activate
```

### 3. Install Dependencies

```
pip install streamlit langchain openai
```

### 4. Add Environment Variables (.env or OS export)

```
OPENAI_API_KEY=your-key
LANGCHAIN_API_KEY=your-key
LANGCHAIN_PROJECT=My-GenAI-Project-OpenAI
LANGCHAIN_TRACING_V2=true
```

---

## Run the App

```
streamlit run app.py
```

---

## Example Code (app.py)

```python
import os
import streamlit as st
from langchain.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import StrOutputParser

# Environment variables
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

os.environ.setdefault("LANGCHAIN_TRACING_V2", "true")
os.environ.setdefault("LANGCHAIN_PROJECT", "My-GenAI-Project-OpenAI")

# Prompt template
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant."),
    ("user", "Question: {question}")
])

# Streamlit UI
st.title("LLM-OPENAI PROJECT - CUSTOM GPT BY TARUN")
input_text = st.text_input("How may I help you?")

# LLM
llm = ChatOpenAI(model_name="gpt-5.1", temperature=0.7)
output_parser = StrOutputParser()
chain = prompt | llm | output_parser

if input_text:
    st.write(chain.invoke({"question": input_text}))
```

---

## Next Steps

- Add chat memory
- Improve UI with chat bubbles
- Add streaming responses
- Add error handling

---

## Author

**Tarun Kumar Rathore**

---
