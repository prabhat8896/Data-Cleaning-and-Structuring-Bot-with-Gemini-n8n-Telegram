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
🛠 How to Run This
Clone or import the provided .json file into n8n

Configure your credentials:

Telegram API (Bot Token)

Gemini API Key via AI Agent

Send a CSV to your bot to test!

Receive cleaned file in seconds 🎉




