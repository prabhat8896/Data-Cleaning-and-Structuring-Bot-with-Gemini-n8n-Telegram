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






{
  "name": "Data Cleaning and Structuring Bot",
  "nodes": [
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.extractFromFile",
      "typeVersion": 1,
      "position": [
        -1180,
        -140
      ],
      "id": "9d8d2c75-4e30-4115-ae64-509afb8e2f3a",
      "name": "Extract from File"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.convertToFile",
      "typeVersion": 1.1,
      "position": [
        -640,
        -100
      ],
      "id": "7a4017f5-16f7-42e6-8f99-53c8dd4f4424",
      "name": "Convert to File"
    },
    {
      "parameters": {
        "url": "=https://api.telegram.org/botYOUR_BOT_TOKEN/getFile?file_id={{ $json[\"message\"][\"document\"][\"file_id\"] }}\n",
        "options": {}
      },
      "id": "524be61f-c9ea-4d41-83f6-333dc3cec739",
      "name": "Get File Path",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 2,
      "position": [
        -1560,
        -100
      ]
    },
    {
      "parameters": {
        "url": "=https://api.telegram.org/file/botYOUR_BOT_TOKEN/{{ $node[\"Get File Path\"].json[\"result\"][\"file_path\"] }}",
        "responseFormat": "file",
        "options": {}
      },
      "id": "e2058ad4-61f7-4c56-aa18-d5ef8e4bc1fc",
      "name": "Download File",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 2,
      "position": [
        -1360,
        -20
      ]
    },
    {
      "parameters": {
        "operation": "sendDocument",
        "chatId": "={{ $node[\"Telegram Trigger1\"].json[\"message\"][\"chat\"][\"id\"] }}",
        "binaryData": true,
        "additionalFields": {
          "fileName": "Cleaned_Data.csv"
        }
      },
      "id": "cb3367bd-127f-48dd-92c5-c3c2e0408adb",
      "name": "Send Document",
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1,
      "position": [
        -460,
        0
      ],
      "webhookId": "d5fbcf85-393e-4d6a-9e14-09f96f383508",
      "credentials": {}
    },
    {
      "parameters": {
        "updates": [
          "message"
        ],
        "additionalFields": {}
      },
      "id": "108b4765-3ca1-4658-a154-6d300b822649",
      "name": "Telegram Trigger1",
      "type": "n8n-nodes-base.telegramTrigger",
      "typeVersion": 1,
      "position": [
        -1800,
        -40
      ],
      "webhookId": "58152a11-9436-4833-8b64-d00a10605bd0",
      "credentials": {}
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "Clean and fix this CSV data",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 2,
      "position": [
        -1020,
        -20
      ],
      "id": "866d9c06-c14a-4897-9eac-9ea55c8a91ea",
      "name": "AI Agent2"
    },
    {
      "parameters": {
        "modelName": "models/gemini-1.5-flash",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        -1000,
        200
      ],
      "id": "08445689-c8e4-43ec-b698-af503f599db8",
      "name": "Google Gemini Chat Model1",
      "credentials": {}
    }
  ],
  "pinData": {},
  "connections": {
    "Extract from File": {
      "main": [
        [
          {
            "node": "AI Agent2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Convert to File": {
      "main": [
        [
          {
            "node": "Send Document",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Telegram Trigger1": {
      "main": [
        [
          {
            "node": "Get File Path",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get File Path": {
      "main": [
        [
          {
            "node": "Download File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download File": {
      "main": [
        [
          {
            "node": "Extract from File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent2": {
      "main": [
        [
          {
            "node": "Convert to File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Gemini Chat Model1": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent2",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "71ae84fb-56b9-4fff-9518-6d75c3b6a5df",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "34bab861c1549c6368dcada4150bc22e12ac5fe43285efb3024f999a48ea99e0"
  },
  "id": "NewRIMA509ErxRMd",
  "tags": []
}







✅ What You Need to Do After Import:
In n8n, go to Credentials:

Add your Telegram Bot as telegramApi

Add your Gemini API key as googlePalmApi

Open the imported workflow

Set the credentials in:

Telegram Trigger

Send Document

Google Gemini Chat Model

Replace YOUR_BOT_TOKEN in the two HTTP Request nodes (if not dynamically handled)
