# AI-question-and-answer-helper
Agentic AI Chat API

A simple agent with tool-calling built using FastAPI, Python & Google Colab (no API keys needed)

 Overview

This project is a beginner-friendly demonstration of how to build a small agentic AI system that:

Detects whether a question is factual

Uses a search tool with a mini knowledge base (KB)

Falls back to a normal conversational reply when needed

Runs fully inside Google Colab

Requires no external API keys

 Features

 FastAPI backend with a /chat endpoint

 Agent architecture (classifier → tool → output)

 Custom search tool with in-memory KB

 +------------------------+
|      User Message      |
+-----------+------------+
            |
            v
+------------------------+
| Intent Detection       |
+-----------+------------+
            |
   +--------+--------+
   |                 |
   v                 v
Factual?         Not Factual
   |                 |
   v                 v
search_tool()   conversational reply
   |                 |
   +--------+--------+
            |
            v
+------------------------+
|     Final Response     |
+------------------------+


No OpenAI / Gemini / Llama API keys required

 Colab auto-test script for screenshots

 Simple, clean & readable Python code

 Project Structure
agent_project/
│
├── agent.py          # Agent logic & tools
├── main.py           # FastAPI app (/chat)
├── test_agent.py     # Automated test runner
└── README.md         # Documentation

 Agent Logic
 1. Intent Detection

A simple rule-based classifier checks if the message is factual.

def is_factual_question(text):
    keywords = ["what", "who", "when", "where", "why", "how"]
    return any(text.lower().startswith(k) for k in keywords)

 2. Search Tool (Knowledge Base)
KB = {
    "python": "Python is a programming language used for development and data science.",
    "ai": "AI stands for Artificial Intelligence — machines that learn from data.",
    "fastapi": "FastAPI is a Python framework for building APIs.",
    "uvicorn": "Uvicorn is an ASGI server used to run FastAPI apps."
}


If the keyword isn’t in the KB → the tool returns None.

 3. Final Response Flow
User message
     ↓
Is it a factual question?
     ↓
 ┌───────────────┬─────────────────┐
 │ YES           │ NO              │
 └───────────────┴─────────────────┘
     ↓                   ↓
search_tool()     conversational reply
     ↓                   ↓
      final response to user
AGENT FLOW DIGRAM

    +------------------------+
|      User Message      |
+-----------+------------+
            |
            v
+------------------------+
| Intent Detection       |
+-----------+------------+
            |
   +--------+--------+
   |                 |
   v                 v
Factual?         Not Factual
   |                 |
   v                 v
search_tool()   conversational reply
   |                 |
   +--------+--------+
            |
            v
+------------------------+
|     Final Response     |
+------------------------+

