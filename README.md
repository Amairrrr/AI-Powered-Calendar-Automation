# 📆 AI Calendar Assistant - Automated Scheduling with n8n & ChatGPT

## 🚀 Overview
Managing calendar events manually can be time-consuming. This project automates the process using an AI-powered workflow. By integrating **n8n**, **ChatGPT**, and **Google Calendar**, users can schedule events simply by sending a chat message.

## 🎯 Key Features
- 📅 **Automated Event Scheduling**: Add new events to Google Calendar via chat.
- 🤖 **AI-Powered Workflow**: Uses ChatGPT for natural language processing.
- 🔄 **Integration with n8n**: No-code automation platform for seamless workflow execution.
- 🛠️ **Error Handling & Troubleshooting**: Built-in logs for debugging.
- ⚙️ **Customizable AI Personality**: Modify system prompts for tailored responses.

## 🛠️ Tech Stack
- **n8n**: No-code workflow automation tool.
- **OpenAI (ChatGPT)**: Processes natural language input.
- **Google Calendar API**: Handles event scheduling.
- **JavaScript (Expressions in n8n)**: Ensures correct date-time handling.

## 📌 Prerequisites
- A **Google Calendar** or **Outlook** account.
- An **n8n** account ([Sign up for free](https://n8n.io/)).
- An **OpenAI API Key** (Claim free credits in n8n).

## 📖 Step-by-Step Guide

### 1️⃣ Set Up Your n8n Workspace
1. Sign up at [n8n.io](https://n8n.io/).
2. Select **Get Started for Free**.
3. Create a new workflow and choose **Start from Scratch**.

### 2️⃣ Add a Chat Trigger
1. Click **Add First Step** → Select **On Chat Message**.
2. This trigger will activate the workflow when a chat message is sent.

### 3️⃣ Integrate AI (ChatGPT)
1. Add a new **AI Agent** node.
2. Configure it as a **Tools Agent** (to interact with Google Calendar).
3. Connect it to **Chat Trigger Node**.
4. Select **OpenAI Chat Model** → Claim **100 free API credits**.

### 4️⃣ Connect to Google Calendar
1. Add a **Google Calendar Node**.
2. Select **+ Create New Credential** → Sign in with Google.
3. Grant access to Google Calendar.
4. Set **Resource** to `Event` and **Operation** to `Create`.

### 5️⃣ Test & Debug the Workflow
1. Open the chat window and send `Hello`.
2. Attempt to schedule an event: `Book a meeting for tomorrow at 10 AM`.
3. If errors occur:
   - Check AI logs to ensure correct data processing.
   - Update **Start Time** and **End Time**: `{{ $fromAI('start_time') }}` & `{{ $fromAI('end_time') }}`.

### 6️⃣ Add a System Message (Fixing Date Issues)
1. Open the AI Agent node.
2. Add a **System Message** with the following prompt:
   ```
   You are a calendar assistant. Your job is to check my availability and create new events for times that my calendar is free. 
   You are to use the Chat Model to process the user's requests, then check availability using the Check Availability tool. 
   Today's date is {{DateTime.now().setZone('TIMEZONE').toFormat('dd LLL yyyy HH:mm:ss')}}.
   ```
3. Set **System Message** to `Expression` mode.

### 7️⃣ Final Testing & Deployment
1. Re-run the chat test to verify correct event scheduling.
2. Check Google Calendar to confirm event creation.
