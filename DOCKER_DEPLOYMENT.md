# 🐳 Docker Deployment Guide - Zero Stress! 

## Why Docker? NO MORE STRESS! 😌

✅ **No server setup** - Docker handles everything  
✅ **Works everywhere** - Local, Digital Ocean, AWS, anywhere  
✅ **One command deployment** - `docker-compose up`  
✅ **Automatic scaling** - Built-in load balancing  
✅ **Easy updates** - Just rebuild and restart  

---

## 🚀 Super Simple Deployment

### Step 1: Setup Environment (2 minutes)

```bash
# 1. Copy the environment file
cp docker.env .env

# 2. Edit .env with your actual values
nano .env
# Add your OpenAI API key and change passwords
```

### Step 2: Local Development (1 command)

```bash
# Start everything locally
docker-compose up --build

# That's it! Your app is running:
# 🌐 Frontend: http://localhost:3000
# 🔧 API: http://localhost:8000
# 📊 Admin: http://localhost:8000/admin
```

### Step 3: Production Deployment (3 commands)

```bash
# 1. Deploy to any server with Docker
docker-compose -f docker-compose.yml --profile production up -d

# 2. Run migrations
docker-compose exec api python manage.py migrate

# 3. Create superuser
docker-compose exec api python manage.py createsuperuser
```

---

## 🌊 Digital Ocean with Docker (5 minutes total!)

### Option A: Docker Droplet (Recommended - Super Easy!)

1. **Create Docker Droplet**
   ```bash
   # Choose "Docker" from marketplace - Docker pre-installed!
   # Size: $12/month (2GB RAM) - perfect for your app
   ```

2. **Deploy Your App**
   ```bash
   # SSH to your droplet
   ssh root@YOUR_DROPLET_IP
   
   # Clone your repo
   git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
   cd YOUR_REPO
   
   # Setup environment
   cp docker.env .env
   nano .env  # Add your values
   
   # Deploy!
   docker-compose up -d --build
   
   # Setup database
   docker-compose exec api python manage.py migrate
   docker-compose exec api python manage.py createsuperuser
   ```

### Option B: Regular Droplet + Install Docker

1. **Create Ubuntu Droplet** ($6/month)

2. **Install Docker (one script)**
   ```bash
   curl -fsSL https://get.docker.com -o get-docker.sh
   sh get-docker.sh
   ```

3. **Deploy** (same as Option A)

---

## 📦 Production Features Included

### 🔧 What's Automatically Configured:
- ✅ **PostgreSQL Database** - Production ready
- ✅ **Redis Caching** - For better performance  
- ✅ **Gunicorn** - Production web server
- ✅ **Nginx** - Static files + reverse proxy
- ✅ **Health Checks** - Auto-restart on failures
- ✅ **Volume Persistence** - Data survives restarts
- ✅ **Security** - Non-root users, proper permissions

### 🔄 Easy Management Commands:

```bash
# View logs
docker-compose logs -f api
docker-compose logs -f frontend

# Update app (when you push new code)
git pull
docker-compose down
docker-compose up -d --build

# Scale your app
docker-compose up -d --scale api=3  # 3 API instances

# Backup database
docker-compose exec db pg_dump -U study_user study_api > backup.sql

# Restore database
docker-compose exec -T db psql -U study_user study_api < backup.sql
```

---

## 💰 Cost Comparison

| Method | Setup Time | Monthly Cost | Complexity |
|--------|------------|--------------|------------|
| **Docker** | 5 minutes | $12/month | ⭐ Easy |
| Manual Setup | 2+ hours | $6/month | ⭐⭐⭐⭐⭐ Complex |

**Docker = Pay $6 more to save hours of stress!** 💆‍♂️

---

## 🌐 Different Deployment Options

### 🏠 Local Development
```bash
docker-compose up
```

### 🚀 Digital Ocean Production
```bash
docker-compose --profile production up -d
```

### ☁️ Other Cloud Providers
- **AWS**: Works with ECS, EC2
- **Google Cloud**: Works with Cloud Run
- **Azure**: Works with Container Instances
- **Heroku**: Works with container stack

---

## 🔧 Environment Variables Guide

```bash
# Required (Must Change!)
SECRET_KEY=make_this_super_long_and_random_50_chars_min
OPENAI_API_KEY=sk-your_actual_openai_key
DB_PASSWORD=strong_database_password

# Optional (Can Keep Defaults)
DOMAIN_NAME=your-domain.com  # Or your droplet IP
SERVER_IP=YOUR_DROPLET_IP
EMAIL_HOST_USER=your-email@gmail.com
```

---

## 🆘 Troubleshooting (Rare Issues)

### App Won't Start?
```bash
# Check logs
docker-compose logs api

# Common fix: rebuild
docker-compose down
docker-compose up --build
```

### Database Issues?
```bash
# Reset database (WARNING: deletes data)
docker-compose down -v
docker-compose up -d
docker-compose exec api python manage.py migrate
```

### Frontend Won't Connect to API?
```bash
# Check if API is running
curl http://localhost:8000/api/health/

# Update frontend environment
# Edit docker-compose.yml -> frontend -> environment -> VITE_API_URL
```

---

## 🎯 Quick Start Checklist

- [ ] Copy `docker.env` to `.env`
- [ ] Add your OpenAI API key to `.env`
- [ ] Run `docker-compose up --build`
- [ ] Visit http://localhost:3000
- [ ] Test AI question generation
- [ ] Deploy to production with `docker-compose --profile production up -d`

---

## 🎉 You're Done!

Your StudyAI app is now running with **zero server configuration stress**! 

**Local**: http://localhost:3000  
**Production**: http://YOUR_DROPLET_IP  

Need help? Just run `docker-compose logs` to see what's happening! 🚀 