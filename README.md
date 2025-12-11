# AI Questionnaire Automation (n8n + WordPress)

This project connects a WordPress-based questionnaire with an AI model using **n8n**.  
User questions are collected on the website, sent to an AI API through n8n, and the responses are delivered back to the user.

> Developed by: **Ghazaleh Ghasemzadeh**

---

## 🧩 Architecture Overview

- **Frontend / WordPress:**
  - A form or plugin collects user questions.
  - The form sends data to n8n via a Webhook or REST API.

- **n8n Workflow:**
  - Receives the question through a **Webhook node**.
  - Passes the question to an **AI API node** (e.g., OpenAI or another LLM).
  - Processes the AI response.
  - Sends the answer back to WordPress, email, or another channel.

---

## 🔧 Components

### 1️⃣ WordPress Integration

- Custom form / shortcode / endpoint to:
  - Send user questions to n8n.
  - Optionally store question & answer in the database.

Possible technologies:
- `wp_remote_post()` for sending data to n8n
- REST API endpoint to receive responses (if needed)

### 2️⃣ n8n Workflow

The workflow (exported as JSON in `/n8n-workflows/ai-questionnaire.json`) typically contains:

- **Webhook node** – entry point for WordPress
- **Function / Set node** – to clean or format the question
- **HTTP Request / AI node** – send question to AI model
- **Function node** – format AI response
- **Return / Webhook Response** – send back the answer

---

## 📦 Installation (n8n)

1. Install and run **n8n** (Docker / local / cloud).
2. Import the workflow JSON file from:  
   `/n8n-workflows/ai-questionnaire.json`
3. Configure:
   - AI API key (e.g. OpenAI key)
   - Webhook URL (copy from n8n)

---

## 🔗 Connecting WordPress and n8n

1. In n8n, copy the **Webhook URL** of your workflow.
2. In WordPress, configure your form or plugin to:
   - Send a POST request to that Webhook URL
   - Include fields like:
     - `user_name` (optional)
     - `user_email` (optional)
     - `question` (required)
3. (Optional) Set up:
   - An email node in n8n to send the answer to the user
   - A callback to WordPress via a REST endpoint to store the answer

---

## 💡 Use Cases

- FAQ form with **AI-generated answers**
- Educational or course-related Q&A system
- Internal assistant for students or customers

---

## 🚀 Future Improvements

- Store question & answer history in WordPress
- Add authentication / rate limiting
- Multi-language support (Persian + English responses)
- Custom prompt templates for different topics

---

## 📝 License

This project was developed as a practical automation for **Maktab Sharif** and can be adapted for similar AI-driven Q&A systems.
