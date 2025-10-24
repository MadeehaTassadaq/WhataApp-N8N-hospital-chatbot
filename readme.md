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
