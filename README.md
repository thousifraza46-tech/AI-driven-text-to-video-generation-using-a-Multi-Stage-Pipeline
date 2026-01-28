# AI-Driven Text-to-Video Generation Platform

An intelligent text-to-video generation system using a multi-stage AI pipeline that converts text prompts into complete videos with script generation, image/video sourcing, audio synthesis, and video editing capabilities.

## 🌟 Features

- **AI Script Generation**: Generate engaging video scripts from simple text prompts
- **Smart Media Sourcing**: Multi-strategy search for relevant images and videos from Pexels
- **Audio Synthesis**: Text-to-speech with multiple voice options
- **Video Editing**: Intuitive drag-and-drop timeline editor
- **AI Chatbot**: Interactive assistant for guidance and support
- **Multi-AI Integration**: Powered by Gemini, Groq, HuggingFace, DeepAI, and more

## 🚀 Quick Start (Local Development)

### Prerequisites

- Node.js 18+ and npm
- Python 3.10+
- API Keys (Gemini, Groq, Pexels, HuggingFace, DeepAI, ElevenLabs)

### Setup

1. **Clone the repository**
```bash
git clone https://github.com/thousifraza46-tech/AI-driven-text-to-video-generation-using-a-Multi-Stage-Pipeline.git
cd AI-driven-text-to-video-generation-using-a-Multi-Stage-Pipeline
```

2. **Install frontend dependencies**
```bash
npm install
```

3. **Setup backend**
```bash
cd backend
pip install -r requirements.txt
```

4. **Configure API keys**
```bash
# Copy template and add your API keys
cp config.template.py config.py
# Edit config.py with your actual API keys
```

5. **Run the application**
```bash
# Terminal 1: Start backend
cd backend
python api_server.py

# Terminal 2: Start frontend
npm run dev
```

6. **Access the application**
- Frontend: http://localhost:8080
- Backend API: http://localhost:5000/api/health

## 📦 Deployment

### Quick Deploy (5 minutes)

See **[QUICK_DEPLOY.md](./QUICK_DEPLOY.md)** for fastest deployment steps.

### Full Deployment Guide

See **[DEPLOYMENT.md](./DEPLOYMENT.md)** for comprehensive deployment instructions including:
- Railway/Render backend deployment
- Vercel/Netlify frontend deployment
- Environment configuration
- CORS setup
- Troubleshooting

### Deployment Summary

1. **Backend** → Railway/Render (Python/Flask)
2. **Frontend** → Vercel/Netlify (React/Vite)
3. **Configure** → Environment variables for API URLs
4. **Test** → Health check endpoint and connection status

## 🛠️ Technologies

### Frontend
- **Framework**: React 18 + TypeScript
- **Build Tool**: Vite 5
- **UI Library**: shadcn/ui + Tailwind CSS
- **State Management**: Zustand
- **Routing**: React Router

### Backend
- **Framework**: Flask (Python)
- **AI Services**: 
  - Google Gemini (Script generation)
  - Groq (Fast LLM)
  - HuggingFace (Image-to-video)
  - DeepAI (Image generation)
  - ElevenLabs (Text-to-speech)
- **Media API**: Pexels (Images & Videos)

## 📁 Project Structure

```
├── src/                    # Frontend React application
│   ├── components/         # Reusable UI components
│   ├── pages/             # Page components
│   ├── services/          # API services
│   ├── config/            # Configuration files
│   └── store/             # State management
├── backend/               # Python Flask backend
│   ├── api_server.py      # Main API server
│   ├── chatbot_engine.py  # AI chatbot
│   ├── script_generator.py# Script generation
│   ├── pexels_video_generator.py # Media search
│   └── modules/           # Additional modules
├── DEPLOYMENT.md          # Comprehensive deployment guide
├── QUICK_DEPLOY.md        # Quick deployment reference
└── README.md              # This file
```

## 🔑 Required API Keys

Get your API keys from:
- **Gemini**: https://makersuite.google.com/app/apikey
- **Groq**: https://console.groq.com/keys
- **Pexels**: https://www.pexels.com/api/
- **HuggingFace**: https://huggingface.co/settings/tokens
- **DeepAI**: https://deepai.org/dashboard/profile
- **ElevenLabs**: https://elevenlabs.io/app/settings/api-keys

## 🧪 Testing

```bash
# Test backend health
curl http://localhost:5000/api/health

# Test frontend build
npm run build
npm run preview
```

## 🐛 Troubleshooting

### Backend not connecting after deployment

1. Check environment variables are set correctly
2. Verify CORS `ALLOWED_ORIGINS` includes frontend URL
3. Test health endpoint: `https://your-backend.com/api/health`
4. Check hosting platform logs for errors

### Assets not loading

1. Verify `VITE_ASSETS_URL` in `.env.production`
2. Check backend serves `/assets` correctly
3. Ensure file paths use absolute paths

See [DEPLOYMENT.md](./DEPLOYMENT.md#troubleshooting) for more solutions.

## 📄 License

This project is open source and available under the MIT License.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support

For issues and questions:
- Check [DEPLOYMENT.md](./DEPLOYMENT.md) for deployment help
- Review [QUICK_DEPLOY.md](./QUICK_DEPLOY.md) for quick reference
- Open an issue on GitHub
- Full backend API integration
- Multi-AI service support
- Advanced media search algorithms
- Production deployment capabilities
