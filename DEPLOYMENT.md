# Deployment Guide

This guide covers deploying both the frontend and backend of the AI-driven Text-to-Video Generation platform.

## 📋 Prerequisites

- Node.js 18+ (for frontend)
- Python 3.10+ (for backend)
- Git
- A hosting platform account (Vercel/Netlify for frontend, Railway/Render/Heroku for backend)

## 🎯 Deployment Architecture

```
┌─────────────────┐         ┌──────────────────┐
│   Frontend      │ ──────> │    Backend       │
│  (React/Vite)   │  API    │  (Flask/Python)  │
│  Port: 3000     │         │   Port: 5000     │
└─────────────────┘         └──────────────────┘
     Vercel/Netlify           Railway/Render
```

---

## 🚀 Backend Deployment

### Option 1: Railway (Recommended)

1. **Create Railway Account**: https://railway.app/

2. **Create New Project**:
   ```bash
   # Install Railway CLI
   npm i -g @railway/cli
   
   # Login
   railway login
   
   # Initialize project
   railway init
   ```

3. **Configure Backend**:
   - Create `Procfile` in backend directory:
     ```
     web: python api_server.py
     ```
   
   - Update `backend/api_server.py` to use environment port:
     ```python
     import os
     
     if __name__ == '__main__':
         port = int(os.environ.get('PORT', 5000))
         app.run(host='0.0.0.0', port=port, debug=False)
     ```

4. **Set Environment Variables in Railway**:
   ```
   GROQ_API_KEY=your_groq_api_key
   GEMINI_API_KEY=your_gemini_api_key
   PEXELS_API_KEY=your_pexels_api_key
   HUGGINGFACE_API_KEY=your_huggingface_api_key
   DEEPAI_API_KEY=your_deepai_api_key
   ELEVEN_LABS_API_KEY=your_elevenlabs_api_key
   PYTHON_VERSION=3.10.0
   ```

5. **Deploy**:
   ```bash
   railway up
   ```

6. **Get Backend URL**: After deployment, Railway will provide a URL like:
   ```
   https://your-project.railway.app
   ```

### Option 2: Render

1. **Create Render Account**: https://render.com/

2. **Create Web Service**:
   - Connect your GitHub repository
   - Set Root Directory: `backend`
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `python api_server.py`

3. **Set Environment Variables** (same as Railway above)

4. **Update `api_server.py`** (same as Railway above)

5. **Deploy**: Render will auto-deploy on push

---

## 🌐 Frontend Deployment

### Option 1: Vercel (Recommended)

1. **Install Vercel CLI**:
   ```bash
   npm i -g vercel
   ```

2. **Update Environment Variables**:
   Edit `.env.production`:
   ```env
   VITE_API_URL=https://your-backend.railway.app/api
   VITE_ASSETS_URL=https://your-backend.railway.app/assets
   ```

3. **Build & Deploy**:
   ```bash
   # Build the project
   npm run build
   
   # Deploy to Vercel
   vercel --prod
   ```

4. **Set Environment Variables in Vercel**:
   - Go to Project Settings → Environment Variables
   - Add:
     ```
     VITE_API_URL=https://your-backend.railway.app/api
     VITE_ASSETS_URL=https://your-backend.railway.app/assets
     ```

### Option 2: Netlify

1. **Install Netlify CLI**:
   ```bash
   npm i -g netlify-cli
   ```

2. **Update `.env.production`** (same as Vercel above)

3. **Create `netlify.toml`**:
   ```toml
   [build]
     command = "npm run build"
     publish = "dist"
   
   [[redirects]]
     from = "/*"
     to = "/index.html"
     status = 200
   ```

4. **Deploy**:
   ```bash
   # Build
   npm run build
   
   # Deploy
   netlify deploy --prod
   ```

---

## 🔧 Backend Configuration Updates

### 1. Update CORS Settings

Edit `backend/api_server.py`:

```python
from flask_cors import CORS

# Update CORS configuration for production
CORS(app, resources={
    r"/api/*": {
        "origins": [
            "http://localhost:8080",  # Development
            "https://your-frontend.vercel.app",  # Production frontend URL
            "https://your-custom-domain.com"  # Custom domain if any
        ],
        "methods": ["GET", "POST", "PUT", "DELETE", "OPTIONS"],
        "allow_headers": ["Content-Type", "Authorization"]
    }
})
```

### 2. Update File Paths for Production

Ensure all file paths use absolute paths or environment-based configuration:

```python
import os

BASE_DIR = os.path.dirname(os.path.abspath(__file__))
ASSETS_DIR = os.path.join(BASE_DIR, 'assets')
VIDEOS_DIR = os.path.join(ASSETS_DIR, 'videos')
IMAGES_DIR = os.path.join(ASSETS_DIR, 'images')
AUDIO_DIR = os.path.join(ASSETS_DIR, 'audio')
```

---

## 🧪 Testing Production Build Locally

### Test Backend:
```bash
cd backend
python api_server.py
```

### Test Frontend Production Build:
```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

Then open: http://localhost:4173

---

## 📝 Post-Deployment Checklist

- [ ] Backend is running and accessible at deployed URL
- [ ] Frontend `.env.production` has correct backend URL
- [ ] All API keys are set in backend environment variables
- [ ] CORS is configured with frontend URL
- [ ] Test health endpoint: `https://your-backend.railway.app/api/health`
- [ ] Test frontend-backend connection in deployed app
- [ ] Check browser console for connection errors
- [ ] Verify asset loading (images, videos, audio)

---

## 🐛 Troubleshooting

### Issue: Frontend can't connect to backend

**Solution**:
1. Check `.env.production` has correct backend URL
2. Verify backend is running: visit `https://your-backend.railway.app/api/health`
3. Check CORS settings in `api_server.py`
4. Check browser console for specific errors

### Issue: 502 Bad Gateway on backend

**Solution**:
1. Check backend logs in Railway/Render dashboard
2. Verify `requirements.txt` has all dependencies
3. Ensure `api_server.py` uses correct port from environment
4. Check if API keys are set correctly

### Issue: Assets not loading

**Solution**:
1. Verify `VITE_ASSETS_URL` in `.env.production`
2. Check backend serves static files correctly
3. Ensure paths in backend use absolute paths
4. Check file permissions on hosting platform

### Issue: API timeouts

**Solution**:
1. Increase timeout settings in hosting platform
2. Optimize API calls (use caching)
3. Consider upgrading hosting plan
4. Check if AI services (Gemini, Groq) are responding

---

## 🔒 Security Best Practices

1. **Never commit API keys** - Use environment variables only
2. **Use HTTPS** - Both frontend and backend should use SSL
3. **Implement rate limiting** - Protect backend from abuse
4. **Validate inputs** - Sanitize all user inputs
5. **Set secure CORS** - Only allow specific origins
6. **Use secrets management** - Railway/Render have built-in secrets management

---

## 📊 Monitoring & Logs

### Railway:
- Dashboard → Project → Deployments → Logs
- Real-time logs available

### Render:
- Dashboard → Web Service → Logs
- Logs are available for last 7 days

### Vercel/Netlify:
- Check deployment logs in dashboard
- Use Vercel Analytics for frontend monitoring

---

## 🔄 Continuous Deployment

### Auto-deploy on Git Push:

1. **Connect Repository** in Vercel/Netlify/Railway/Render
2. **Set Auto-deploy branch** (usually `main`)
3. **Configure build settings**
4. Push to GitHub → Automatic deployment

---

## 💡 Optimization Tips

1. **Enable caching** - Cache API responses
2. **Use CDN** - For assets (images, videos)
3. **Compress assets** - Reduce file sizes
4. **Lazy loading** - Load components on demand
5. **Database** - Consider using PostgreSQL for data persistence
6. **Redis** - For caching and session management

---

## 📞 Need Help?

- **Backend Issues**: Check Railway/Render logs
- **Frontend Issues**: Check browser console
- **API Issues**: Test endpoints with Postman
- **CORS Issues**: Verify origin settings

---

## 🎉 Success!

Your AI-driven text-to-video platform should now be live! 

**Frontend**: https://your-project.vercel.app
**Backend**: https://your-project.railway.app
**Health Check**: https://your-project.railway.app/api/health
