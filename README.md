# Online_Shopping_Agent
An AI-Powered Online Shopping Agent built with Python, Streamlit, LangChain, Groq LLM,Fast API and SQLite. It enables natural language and image-based product search, providing personalized recommendations based on price, ratings, reviews, and user preferences for a smart, seamless shopping experience.

# 🛒 AI Shopping Agent

An AI-powered shopping assistant that helps users discover products through natural language conversations and image-based search. Built using **Python, Streamlit, LangChain, Groq LLM, and SQLite**, the agent provides intelligent product recommendations based on user preferences, product ratings, reviews, and pricing.

---

## 🚀 Features

### 🔍 Product Search
- Search products using natural language.
- Filter by price, category, ratings, and organic products.
- Intelligent recommendations using Groq LLM.

### 📸 Image-Based Shopping
- Upload a product image.
- AI analyzes the image and finds similar products available in the store.

### ⭐ Product Recommendations
- Personalized recommendations.
- Considers product ratings, reviews, pricing, and user requirements.
- Displays products in an easy-to-read numbered list.

---

# 🧠 Advanced Features

## 1. Memory & Personalization

### 📦 Order History Summary
The agent remembers previous purchases by querying the **Orders** table.

Example:

```
What have I ordered before?
```

The assistant summarizes previous purchases and provides recommendations based on shopping history.

---

### ❤️ User Preferences

The shopping assistant stores user preferences so customers don't need to repeat them.

Examples:

- Prefer Organic Products
- Budget under $20
- Favorite categories
- Preferred brands

Example:

```
I always prefer organic products.
```

Future searches automatically apply these preferences.

---

# 🛡️ Guardrails

The application includes an input validation layer before the LLM processes requests.

Supported requests include:

- Product search
- Shopping advice
- Product comparison
- Order history
- Product recommendations

Unsupported requests are politely rejected.

Example:

```
Write me a poem.
```

Response:

```
I'm designed to help with shopping-related questions.
Please ask about products, prices, or recommendations.
```

---

# 📊 Evaluation

## Tool Call Accuracy Evaluation

A test suite validates whether the agent selects the correct tool and parameters.

Example Test Cases

| User Query | Expected Tool |
|------------|---------------|
| Organic honey under $20 | search_products(is_organic=True,max_price=20) |
| Coffee above 4.5 rating | search_products(min_rating=4.5) |
| Best organic tea | search_products(is_organic=True) |

The evaluation ensures:

- Correct tool selection
- Correct parameter extraction
- Reliable agent behavior

---

## Response Quality Evaluation

The project uses an **LLM-as-a-Judge** approach to evaluate generated responses.

Evaluation Metrics

- Relevance
- Correctness
- Product Accuracy
- Format Compliance
- Recommendation Quality
- User Satisfaction

Responses are scored automatically to ensure high-quality shopping assistance.

---

# 🏗️ Tech Stack

- Python
- Streamlit
- LangChain
- Groq LLM
- SQLite
- LangGraph
- Python-dotenv

---

# 📂 Project Structure

```
shopping-agent/
│
├── app.py
├── shopping_agent.py
├── reviews_api.py
├── store.db
├── requirements.txt
├── .env
└── README.md
```

---

# 🎯 Future Improvements

- Voice-based shopping assistant
- Multi-language support
- Product image generation
- Real-time inventory updates
- Shopping cart integration
- Payment gateway
- User authentication
- Recommendation dashboard
- Order tracking
- AI price comparison

---

# 👨‍💻 Author

Developed as an **Agentic AI Shopping Assistant** project demonstrating:

- Large Language Models (LLMs)
- Agentic AI
- LangChain Agents
- Tool Calling
- Memory
- Guardrails
- AI Evaluation
- Personalized Recommendations
- Image-Based Product Search
