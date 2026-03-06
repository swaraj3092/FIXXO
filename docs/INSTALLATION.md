# Installation Guide

Complete setup instructions for local development.

## Prerequisites

- Python 3.8+
- Git
- Twilio account
- Supabase account
- Resend account

## Step-by-Step Setup

### 1. Clone Repository
```bash
git clone https://github.com/swaraj3092/smart-hostel-complaint-system.git
cd smart-hostel-complaint-system
```

### 2. Create Virtual Environment
```bash
python -m venv venv

# Activate:
# Windows:
venv\Scripts\activate

# Mac/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Services

#### Twilio (WhatsApp)
1. Go to https://console.twilio.com
2. Get Account SID and Auth Token
3. Go to Messaging → Try it out → Send a WhatsApp message
4. Note sandbox number: `+1 415 523 8886`

#### Supabase (Database)
1. Go to https://supabase.com
2. Create new project
3. Go to SQL Editor
4. Run the schema from `docs/database-schema.sql`
5. Copy Project URL and Service Role Key

#### Resend (Email)
1. Go to https://resend.com
2. Create API key
3. Copy key

### 5. Configure Environment
```bash
cp .env.example .env
```

Edit `.env`:
```
TWILIO_ACCOUNT_SID=your_sid
TWILIO_AUTH_TOKEN=your_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your_service_role_key

RESEND_API_KEY=re_your_key

BASE_URL=http://localhost:5000
```

### 6. Run Application
```bash
python src/app.py
```

Should see:
```
* Running on http://127.0.0.1:5000
```

### 7. Expose to Internet (Testing)

**Option A: ngrok**
```bash
ngrok http 5000
```

**Option B: Deploy to Render** (see DEPLOYMENT.md)

### 8. Configure Twilio Webhook

1. Copy your ngrok/Render URL
2. Go to Twilio Sandbox Settings
3. Set "When a message comes in":
```
   https://your-url.ngrok.io/webhook
```

### 9. Test

Send WhatsApp message to `+1 415 523 8886`:
```
join <your-sandbox-code>
```

Then:
```
The WiFi is not working in Room 305 urgent
```

Should receive instant reply with complaint ID!

## Troubleshooting

**Issue:** No response from WhatsApp
- Check Flask is running
- Check ngrok/webhook URL is correct
- Check Twilio webhook is saved

**Issue:** Database errors
- Verify Supabase credentials
- Check schema is created

**Issue:** Email not sending
- Verify Resend API key
- Check sender email is verified