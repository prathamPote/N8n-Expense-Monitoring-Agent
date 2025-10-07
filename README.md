# 📊 AI-Powered Expense Tracking Automation (n8n Workflow)

An automated **expense tracking system** built using **n8n**, integrating **AI-powered SMS parsing**, **Google Sheets**, and **Discord/Gmail notifications**.  
This workflow automatically extracts expense details from incoming SMS messages and logs them into Google Sheets — no manual data entry needed!

---

## 🚀 Features

- 📨 **Automated SMS Capture**  
  Captures incoming transaction messages via a webhook (from Tasker or other automation tools).

- 🤖 **AI Expense Extraction**  
  Uses a **LangChain + OpenRouter LLM** agent to:
  - Identify whether a message is an expense or income  
  - Extract key fields (expense name, value, date, category)  
  - Categorize expenses (Food, Bills, Shopping, etc.)  
  - Ignore OTPs and unrelated messages  

- 📄 **Smart Logging**  
  Appends valid expense entries to a **Google Sheet** with the following columns:  
  `Expense ID`, `Expense Name`, `Expense Value`, `Date`, `Running Total`, `Category`

- 🔔 **Automated Notifications**  
  - Sends confirmation via **Gmail**  
  - Sends summary message via **Discord DM**  
  - Notifies for **non-expense messages** for review  

---

<img width="1496" height="587" alt="image" src="https://github.com/user-attachments/assets/d1db110e-1c54-4526-b6d3-31bea4b6b660" />

---

## 🧩 Integrations

- 🧠 **OpenRouter API** — LLM model for natural language parsing (`deepseek/deepseek-chat-v3.1:free`)  
- 📊 **Google Sheets API** — Logs structured expense entries  
- 💬 **Discord Bot (OAuth2)** — Sends user notifications  
- 📧 **Gmail API** — Email confirmations  
- 📱 **Tasker (Android)** — For forwarding SMS data to n8n webhook *(optional)*  

---

## ⚙️ Setup Instructions

1. **Import the workflow** into your n8n instance (`Expense-tracking.json`).
2. Configure credentials for:
   - OpenRouter API  
   - Google Sheets (Service Account)  
   - Discord OAuth2  
   - Gmail OAuth2
3. Update:
   - Google Sheet ID and Sheet name  
   - Discord user ID and server ID  
4. Deploy the workflow and copy your **Webhook URL**.
5. Configure **Tasker** or any SMS-forwarding tool to send POST requests to this webhook.
6. Test the setup by sending a sample message from your banking SMS.

---

## 🧾 Example

### 📥 Input (Webhook Payload)

```json
{
  "text": "Hi, we have processed Rs. 349.0 for your Airtel Mobile 9886564443. The payment will be updated within 15 minutes.",
  "from": "AX-AIRINF",
  "date": "2025-07-10"
}
