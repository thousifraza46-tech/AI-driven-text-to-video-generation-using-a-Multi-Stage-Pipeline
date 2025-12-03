# 🚀 Quick Deployment Guide

This is a quick reference for deploying your AI Text-to-Video platform. For detailed instructions, see [DEPLOYMENT.md](./DEPLOYMENT.md).

## ⚡ Quick Steps

### 1. Deploy Backend (Railway - Fastest)

```bash
# Install Railway CLI
npm i -g @railway/cli

# Login to Railway
railway login

# Deploy from backend directory
cd backend
railway init
railway up
```

**Set these environment variables in Railway dashboard:**
```
PORT=5000
ENVIRONMENT=production
GROQ_API_KEY=your_key_here
GEMINI_API_KEY=your_key_here
PEXELS_API_KEY=your_key_here
HUGGINGFACE_API_KEY=your_key_here
DEEPAI_API_KEY=your_key_here
ELEVEN_LABS_API_KEY=your_key_here
ALLOWED_ORIGINS=https://your-frontend-url.vercel.app
```

**Copy your Railway backend URL** (e.g., `https://your-app.railway.app`)

---

### 2. Configure Frontend

Update `.env.production` with your backend URL:

```env
VITE_API_URL=https://your-app.railway.app/api
VITE_ASSETS_URL=https://your-app.railway.app/assets
```

---

### 3. Deploy Frontend (Vercel - Fastest)

```bash
# Install Vercel CLI
npm i -g vercel

# Build and deploy
npm run build
vercel --prod
```

In Vercel dashboard, add environment variables:
```
VITE_API_URL=https://your-app.railway.app/api
VITE_ASSETS_URL=https://your-app.railway.app/assets
```

---

## ✅ Verify Deployment

1. **Check Backend Health:**
   ```
   https://your-app.railway.app/api/health
   ```
   Should return: `{"status": "healthy", "message": "AI Video Generation API is running"}`

2. **Check Frontend:**
   - Open your Vercel URL
   - Check connection indicator in top bar
   - Should show "Connected" status

3. **Test Full Flow:**
   - Go to "Generate Video" page
   - Enter a prompt
   - Generate video
   - Verify images/videos load correctly

---

## 🐛 Common Issues

### Frontend can't connect to backend
- ✅ Check `.env.production` has correct backend URL
- ✅ Verify CORS: `ALLOWED_ORIGINS` in Railway includes your Vercel URL
- ✅ Check backend health endpoint is accessible

### 502 Bad Gateway
- ✅ Check Railway logs for errors
- ✅ Verify all API keys are set
- ✅ Ensure `PORT` environment variable is set

### Assets not loading
- ✅ Check `VITE_ASSETS_URL` points to backend
- ✅ Verify backend `/assets` endpoint works
- ✅ Check file permissions

---

## 📚 Need More Help?

See [DEPLOYMENT.md](./DEPLOYMENT.md) for:
- Alternative hosting options (Render, Netlify)
- Detailed configuration steps
- Troubleshooting guide
- Security best practices
- Monitoring and optimization tips

---

## 🎉 Done!

Your app should now be live:
- **Frontend:** `https://your-project.vercel.app`
- **Backend:** `https://your-app.railway.app`
- **API:** `https://your-app.railway.app/api/`
