# 🔐 Environment Setup Guide

## ✅ Your settings.py is now SECURE! 

Your Django settings have been updated to use environment variables instead of hardcoded values. Here's how to set it up:

---

## 🚀 Quick Setup (2 minutes)

### Step 1: Create Environment File
```bash
cd study-api
cp env.local.example .env
```

### Step 2: Add Your OpenAI API Key
```bash
# Edit .env file
nano .env

# Replace this line:
OPENAI_API_KEY=sk-your_openai_api_key_here

# With your actual key:
OPENAI_API_KEY=sk-proj-your-actual-key-here
```

### Step 3: Test Everything
```bash
# Run the setup script
./setup.sh

# Or manually:
python manage.py runserver

# Test health check:
curl http://localhost:8000/api/health/
```

---

## 🔑 Get OpenAI API Key

1. **Go to**: https://platform.openai.com/api-keys
2. **Login** to your OpenAI account
3. **Click**: "Create new secret key"
4. **Copy** the key (starts with `sk-`)
5. **Paste** into your `.env` file

---

## 📁 Environment Files Overview

```
study-api/
├── .env                    # Your actual values (NEVER commit!)
├── env.local.example       # Template for local development
├── env.example            # Template for production
└── docker.env             # Template for Docker
```

---

## 🛡️ Security Benefits

### ✅ Before (Insecure):
```python
OPENAI_API_KEY = 'sk-proj-actual-key-in-code'  # 😱 EXPOSED!
SECRET_KEY = 'hardcoded-secret'                # 😱 EXPOSED!
```

### ✅ After (Secure):
```python
OPENAI_API_KEY = config('OPENAI_API_KEY', default='')  # 🔒 SECURE!
SECRET_KEY = config('SECRET_KEY', default='...')       # 🔒 SECURE!
```

### 🔒 What's Protected:
- **OpenAI API Key** - From environment variables
- **Secret Key** - From environment variables  
- **Database Credentials** - From environment variables
- **JWT Signing Key** - From environment variables
- **AWS Credentials** - From environment variables

---

## 🚨 Validation & Warnings

Your updated settings include automatic validation:

### ✅ Development Mode:
```bash
⚠️  WARNING: OPENAI_API_KEY not found in environment variables!
   Add your OpenAI API key to .env file for AI features to work.
```

### ✅ Production Mode:
```bash
ValueError: OPENAI_API_KEY environment variable is required!
```

### ✅ Health Check:
```bash
curl http://localhost:8000/api/health/

{
  "status": "healthy",
  "debug": true,
  "openai_configured": true,
  "database": "connected",
  "openai_status": "configured",
  "openai_message": "API key is set"
}
```

---

## 🐳 Docker Support

Your environment setup works seamlessly with Docker:

```bash
# Copy Docker environment template
cp docker.env .env

# Add your OpenAI key to .env
nano .env

# Run with Docker
docker-compose up --build
```

---

## 🔧 Available Environment Variables

```bash
# Django Core
SECRET_KEY=your-secret-key
DEBUG=True/False
ALLOWED_HOSTS=localhost,yourdomain.com

# Database (SQLite default, PostgreSQL for production)
DB_ENGINE=django.db.backends.sqlite3
DB_NAME=db.sqlite3
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_HOST=localhost
DB_PORT=5432

# OpenAI (REQUIRED for AI features)
OPENAI_API_KEY=sk-your-api-key

# JWT Authentication
JWT_SIGNING_KEY=your-jwt-key

# CORS (for frontend)
CORS_ALLOW_ALL_ORIGINS=False
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173

# AWS S3 (Optional)
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_STORAGE_BUCKET_NAME=your-bucket
AWS_S3_REGION_NAME=us-east-1
```

---

## 🎯 Next Steps

1. ✅ **Setup environment**: `cp env.local.example .env`
2. ✅ **Add OpenAI key**: Edit `.env` file  
3. ✅ **Test setup**: `python manage.py runserver`
4. ✅ **Check health**: Visit http://localhost:8000/api/health/
5. ✅ **Test AI features**: Upload a document and generate questions!

**Your API is now secure and production-ready! 🚀** 