# 🏥 Twilio WhatsApp Chatbot – AI Appointment Booking System

An **AI-powered WhatsApp chatbot** built with **n8n**, **Twilio**, **Google Gemini (PaLM)**, and **Google Sheets**, designed for **automated hospital appointment booking** and **doctor availability lookup**.

---

## 🚀 Features

### 💬 AI-Powered Chatbot (Google Gemini)
- Handles three main intents:
  1. **General Chat** – Answers questions about hospital services, timings, or facilities.  
  2. **Doctor Lookup** – Fetches doctor schedules from Google Sheets.  
  3. **Appointment Booking** – Collects patient details and creates a structured booking request.

### 📅 Google Sheets Integration
- **Doctor Availability Sheet** – Reads doctor timings and availability.  
- **Patient Booking Sheet** – Appends or updates patient appointment data.

### 📧 Automated Gmail Confirmation
- Sends a confirmation email to the patient once the appointment is successfully booked.

### 🧠 Memory System (PostgreSQL)
- Maintains chat context between user messages for a natural conversational experience.

### 🌐 Webhook Endpoint
- Connects with Twilio WhatsApp API to receive and send messages in real time.

---

## ⚙️ Tech Stack

| Component | Purpose |
|------------|----------|
| **n8n** | Orchestrates the automation workflow |
| **Google Gemini (PaLM)** | Natural language understanding and intent classification |
| **Google Sheets** | Stores doctor and appointment data |
| **PostgreSQL** | Maintains user session memory |
| **Twilio WhatsApp API** | Sends and receives WhatsApp messages |
| **Gmail API** | Sends appointment confirmation emails |

---

## 🔄 Workflow Overview

1. **Webhook Trigger (Twilio WhatsApp Message)**  
   Receives the incoming WhatsApp message via Twilio and passes it to the chatbot workflow.

2. **WhatsApp Agent (Google Gemini)**  
   Analyzes user intent and outputs structured JSON following this schema:

   ```json
   {
     "type": "chat" | "doctor_lookup" | "booking_request",
     "message": "Short reply to user",
     "data": {
       "Doctor Name": "",
       "Date": "",
       "Time": "",
       "Patient Name": "",
       "Email": "",
       "Phone": "",
       "Status": ""
     }
   }
   

 3.Code Node (JSON Cleanup)
Cleans and validates the AI output into strict JSON.

4.If Node
Routes based on intent:

booking_request → triggers appointment creation and confirmation.

chat or doctor_lookup → sends appropriate responses.

5.AI Agent 1 (Action Agent)

Appends appointment to Google Sheets

Sends Gmail confirmation

Notifies the patient via WhatsApp

6.HTTP Request (Twilio)
Sends the response message back to the user on WhatsApp.
📊 Data Sheets
Sheet Name	Description	Example Link
Doctors schedule	Contains doctor availability and timings	fictional_doctors_pakistan

Patient Booking Data	Stores confirmed appointment info	Patient Booking Data
🧩 Credentials Required

Before importing the workflow, set up these credentials in n8n:

Credential	Purpose
Google Sheets OAuth2 API	For reading/writing to Google Sheets
Google Palm API (Gemini)	For chatbot intelligence
Postgres Account	For conversation memory
Gmail OAuth2	To send confirmation emails
HTTP Basic Auth (Twilio)	To connect with Twilio WhatsApp API
🛠️ Installation

Import the provided JSON workflow file into your n8n instance.

Configure all credentials listed above.

Deploy your Webhook URL in Twilio WhatsApp sandbox or live number.

Test the workflow by sending a WhatsApp message such as:

"Book an appointment with Dr. Ayesha for Monday at 10 AM."

📬 Example Conversation

User:

Hi, I want to book an appointment with Dr. Ayesha on Monday.

Bot:

Great! Could you please share your name, email, and phone number?

User:

Madeeha Tassadaq, madeeha50@yahoo.com
, 03264897218

Bot:

Thanks! Your appointment with Dr. Ayesha is confirmed for Monday at 10 AM. You’ll receive a confirmation email shortly. ✅

🧠 Architecture Diagram
Twilio WhatsApp → Webhook → WhatsApp Agent → Code Node → IF (Intent)  
     └──→ AI Agent 1 → Google Sheets → Gmail → Twilio (Response)

👩‍⚕️ Author

Madeeha Tassadaq
AI & Automation Developer
📧 madeeha50@yahoo.com

📜 License

This project is released under the MIT License.
Feel free to fork, modify, and use for educational or non-commercial projects.

⭐ If you found this helpful, star the repository on GitHub!

---

Would you like me to include a small **architecture diagram image** or keep it as plain text (for Markdown-only simplicity)?  
I can also generate and attach a `.md` file ready for upload.
