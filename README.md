# Data-Cleaning-and-Structuring-Bot-with-Gemini-n8n-Telegram
A fully automated Telegram bot powered by **n8n** and **Google Gemini AI**, designed to clean and standardize messy CSV files sent by users.

---

## 🚀 Features

- 📥 Accepts `.csv` file uploads via Telegram
- 🔍 Cleans data with Gemini AI (fixes casing, phone/email formats, typos)
- 📄 Returns a cleaned CSV file to the user
- 🧠 Built using n8n with no code or minimal scripting
- 🔒 Secure, lightweight, and runs on your own infrastructure

---

## 🔧 Tech Stack

- [n8n](https://n8n.io/) – Visual workflow automation tool
- [Telegram Bot API](https://core.telegram.org/bots/api) – File transfer and chat interaction
- [Google Gemini 1.5 Flash](https://ai.google.dev/) – AI-based data cleaning via prompt
- Custom expressions in n8n (Handlebars templating)

---

## 📁 Project Workflow

```mermaid
graph TD
  A[User sends CSV to Telegram bot] --> B[Get file path from Telegram API]
  B --> C[Download binary file]
  C --> D[Parse CSV (Spreadsheet File)]
  D --> E[Send to Gemini via AI Agent]
  E --> F[Create new cleaned file]
  F --> G[Send back cleaned CSV via Telegram]
