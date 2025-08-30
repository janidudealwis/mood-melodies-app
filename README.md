# 🎵 Mood Melodies App

**AI-Powered Music Recommendation App Based on Facial Emotion Analysis**

A React Native mobile application that captures your photo, analyzes your mood using AI facial recognition, and provides personalized music playlists from Spotify and other free music sources.

![Mood Melodies App](./assets/images/Logo%20Trans.png)

## 📱 Features

### 🎯 Core Functionality

- **📸 Photo Capture**: Take photos using device camera
- **🤖 AI Mood Analysis**: Real-time facial emotion detection using face-api.js
- **🎵 Smart Music Recommendations**: Curated playlists based on detected emotions
- **🎧 Integrated Music Player**: Play, pause, skip, and control music playback
- **💾 Mood History**: Track your emotional journey over time
- **🔐 User Authentication**: Secure login/signup with Supabase

### 🎭 Supported Emotions

- **😊 Happy** - Upbeat, energetic tracks
- **😢 Sad** - Melancholic, emotional ballads
- **😠 Angry** - Rock, intense music
- **😌 Calm** - Peaceful, relaxing sounds
- **😰 Anxious** - Soothing, calming melodies
- **😲 Surprised** - Discovery mix, unexpected genres
- **🤢 Disgusted** - Alternative, raw music

### 🎼 Music Sources

- **🎯 Primary**: Spotify Web API (10M+ tracks)
- **🔄 Fallback**: Curated free audio for guaranteed playback
- **🎚️ Quality**: High-quality audio streaming with metadata

## 🛠️ Tech Stack

### 📱 Frontend

- **React Native** with Expo SDK 53
- **TypeScript** for type safety
- **Expo Router** for navigation
- **NativeWind** for styling
- **Expo Camera** for photo capture
- **Expo AV** for audio playback

### 🧠 AI & Backend

- **face-api.js** for facial emotion recognition
- **Node.js/Express** API server for mood analysis
- **Supabase** for authentication and data storage
- **ngrok** for tunnel access to local API

### 🎵 Audio Integration

- **Spotify Web API** with Client Credentials flow
- **Reliable fallback system** with tested audio URLs
- **Cross-platform audio playback** via Expo AV

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18+ and npm
- **Expo CLI**: `npm install -g @expo/cli`
- **Android Studio** (for Android) or **Xcode** (for iOS)
- **Expo Go** app on your mobile device

### 1. Clone & Install

```bash
git clone https://github.com/sandunMadhushan/mood-melodies-app.git
cd mood-melodies-app
npm install
cd face-api-service
npm install
cd ..
```

### 2. Environment Setup

#### Supabase Configuration

1. Create account at [supabase.com](https://supabase.com)
2. Create new project
3. Update `lib/supabase.ts` with your credentials:

```typescript
const supabaseUrl = 'YOUR_SUPABASE_URL';
const supabaseAnonKey = 'YOUR_SUPABASE_ANON_KEY';
```

#### ngrok Setup (for real mood analysis)

1. Create account at [ngrok.com](https://ngrok.com)
2. Get your authtoken from dashboard
3. Configure ngrok:

```bash
./tools/ngrok/ngrok.exe authtoken YOUR_AUTHTOKEN
```

#### Spotify API Setup (Optional)

1. Go to [Spotify Developer Dashboard](https://developer.spotify.com/dashboard)
2. Create new app
3. Update music service configuration

For detailed Spotify setup, see: [docs/markdown/SPOTIFY-SETUP.md](./docs/markdown/SPOTIFY-SETUP.md)

### 3. One-Command Startup 🚀

**This is the easiest way to start everything:**

```bash
# Windows
./start-all.bat

# Linux/Mac
./start-all.sh
```

This automatically starts:

1. 🤖 Face API Service (localhost:3001)
2. 🌐 ngrok tunnel (public access)
3. 📱 Expo development server (tunnel mode)
4. 🔄 Auto-updates app with ngrok URL

### 4. Manual Startup (Alternative)

If you prefer to start services individually:

```bash
# Terminal 1: Start Face API Service
node face-api-service/server-simple.js

# Terminal 2: Start ngrok tunnel
./tools/ngrok/ngrok.exe http 3001

# Terminal 3: Update app with ngrok URL
node tools/ngrok/update-ngrok-url.js

# Terminal 4: Start Expo
npx expo start --tunnel --clear
```

## 📱 Installation & Usage

### Development Testing

1. **Install Expo Go** on your mobile device
2. **Run startup script**: `./start-all.bat` or `./start-all.sh`
3. **Scan QR code** from Expo terminal
4. **Allow camera permissions** when prompted
5. **Test mood analysis** by taking a selfie

### Production Build

```bash
# Android APK
npx expo build:android

# iOS IPA
npx expo build:ios
```

## 🎯 App Flow

### 1. Authentication

- **Sign up** with email/password
- **Login** to existing account
- **Secure session** management with Supabase

### 2. Mood Capture

- **📸 Take Photo**: Capture using device camera
- **🤖 AI Analysis**: Real-time mood detection via ngrok tunnel
- **📊 Results**: View detected emotion with confidence score

### 3. Music Discovery

- **🎵 Smart Playlists**: Auto-generated based on detected mood
- **🎯 Spotify Integration**: Real tracks with metadata
- **🔄 Fallback System**: Guaranteed music playback

### 4. Music Experience

- **🎧 Integrated Player**: Play/pause, seek, skip
- **📱 Intuitive Controls**: Seamless mobile experience
- **💾 History**: Track your mood and music journey

## 🏗️ Architecture

### Project Structure

```
mood-melodies-app/
├── 🚀 start-all.sh             # One-command startup (Linux/Mac)
├── 🚀 start-all.bat            # One-command startup (Windows)
├── 📖 README.md                # This file
├── 📱 app/                     # App screens (Expo Router)
│   ├── (auth)/                # Authentication screens
│   │   ├── login.tsx          # Login screen
│   │   └── signup.tsx         # Signup screen
│   ├── (tabs)/                # Main app tabs
│   │   ├── index.tsx          # Home/Dashboard
│   │   ├── capture.tsx        # Photo capture
│   │   ├── music.tsx          # Music player
│   │   ├── favorites.tsx      # Saved favorites
│   │   └── profile.tsx        # User profile
│   ├── analyzing.tsx          # Mood analysis screen
│   ├── mood-result.tsx        # Analysis results
│   └── player.tsx             # Music player screen
├── 📡 lib/                     # Core services
│   ├── supabase.ts            # Database client
│   ├── musicService.ts        # Music API integration
│   ├── faceApiService.ts      # Mood analysis client
│   └── dynamicNetworkDiscovery.ts # Network discovery
├── 🧩 components/              # Reusable UI components
├── 🔧 context/                 # React context providers
│   └── AuthContext.tsx        # Authentication context
├── 🤖 face-api-service/        # Node.js API server
│   ├── server-simple.js       # Express server
│   ├── get-ngrok-url.js       # ngrok URL fetcher
│   └── package.json           # API dependencies
├── 📚 docs/                    # Documentation
│   ├── DEV-GUIDE.md           # Development guide
│   └── markdown/              # All documentation files
├── 📋 scripts/                 # Development utilities
│   ├── startup/               # Legacy startup scripts
│   ├── cleanup-port.sh        # Port management
│   ├── find-ip.js            # Network discovery
│   └── test-network.js       # Network testing
├── 🛠️ tools/                   # Development tools
│   └── ngrok/                 # ngrok tunnel tools
│       ├── ngrok.exe          # ngrok executable
│       └── update-ngrok-url.js # Auto URL updater
└── 🎨 assets/                  # Images and static files
```

### Key Services

#### Face API Service (`face-api-service/`)

- **Express server** for mood analysis
- **face-api.js integration** for emotion detection
- **Image processing** and confidence scoring
- **RESTful API** endpoints
- **Realistic mock analysis** for development

#### Dynamic Network Discovery (`lib/dynamicNetworkDiscovery.ts`)

- **Automatic ngrok URL detection**
- **Fallback to localhost** for development
- **Tunnel mode optimization**
- **Enhanced error handling**

#### Music Service (`lib/musicService.ts`)

- **Spotify API integration** with access token management
- **Smart fallback system** for guaranteed playback
- **Cross-platform audio** playback via Expo AV
- **Error handling** and retry logic

## 🔧 Configuration

### Music Service Configuration

The app uses a robust music system with multiple sources:

1. **Primary**: Spotify Web API
2. **Fallback**: Tested audio URLs for guaranteed playback
3. **Mood Mapping**: Smart genre selection based on emotions

### API Endpoints

- **Mood Analysis**: `http://localhost:3001/analyze-mood`
- **Health Check**: `http://localhost:3001/health`
- **ngrok Tunnel**: Dynamic URL via tunnel discovery

### ngrok Configuration

The app automatically detects and uses ngrok tunnel URLs for mobile access:

- **Automatic discovery** of ngrok public URL
- **Header injection** for ngrok compatibility
- **Fallback handling** when tunnel is unavailable

## 🐛 Troubleshooting

### Common Issues

#### 1. Face API Service Issues

```bash
# Check if service is running
curl http://localhost:3001/health

# Kill port conflicts
npx kill-port 3001

# Start service manually
node face-api-service/server-simple.js
```

#### 2. ngrok Tunnel Issues

```bash
# Configure authtoken
./tools/ngrok/ngrok.exe authtoken YOUR_TOKEN

# Start tunnel manually
./tools/ngrok/ngrok.exe http 3001

# Update app with new URL
node tools/ngrok/update-ngrok-url.js
```

#### 3. Camera Permissions

```bash
# Add to app.json
"permissions": ["CAMERA", "CAMERA_ROLL"]
```

#### 4. Audio Playback Issues

- Ensure **Expo AV** is properly installed
- Check **audio URLs** are accessible
- Verify **device audio settings**

#### 5. Network Connectivity

```bash
# Test network connectivity
node scripts/test-network.js

# Find local IP
node scripts/find-ip.js
```

### Debug Mode

Enable detailed logging for troubleshooting:

```typescript
// Enhanced logging in faceApiService.ts
console.log('🔍 Network discovery result:', result);
console.log('📡 Using endpoint:', endpoint);
```

### Service Health Checks

```bash
# Check Face API health
curl http://localhost:3001/health

# Check ngrok tunnel (replace with your URL)
curl -H "ngrok-skip-browser-warning: any" https://your-ngrok-url.ngrok-free.app/health

# Test mood analysis
curl -X POST -H "Content-Type: application/json" \
  -d '{"image":"base64_image_data"}' \
  http://localhost:3001/analyze-mood
```

## 📚 Documentation

### Additional Guides

- **[Development Guide](./docs/DEV-GUIDE.md)** - Complete development setup
- **[Spotify Setup Guide](./docs/markdown/SPOTIFY-SETUP.md)** - Spotify API integration
- **[Music Playback Guide](./docs/markdown/MUSIC-PLAYBACK-GUIDE.md)** - Audio system details
- **[Testing Guide](./docs/markdown/TESTING-GUIDE.md)** - QA and testing procedures
- **[Startup Guide](./docs/markdown/STARTUP-GUIDE.md)** - Detailed setup instructions
- **[Tunnel Mode Guide](./docs/markdown/TUNNEL-MODE.md)** - ngrok tunnel configuration

### API Reference

- **Mood Analysis**: POST `/analyze-mood` with image data
- **Health Check**: GET `/health` for service status
- **Music Search**: Spotify Web API integration
- **User Auth**: Supabase authentication flow

## 🚀 Deployment

### Mobile App Stores

```bash
# Build for production
npx expo build:android
npx expo build:ios

# Submit to stores
npx expo submit:android
npx expo submit:ios
```

### API Server Deployment

Deploy the face-api-service to cloud platforms:

- **Heroku**: `git push heroku main`
- **Vercel**: `vercel deploy`
- **Railway**: Connect GitHub repository

Update the app configuration to use production API endpoint.

## 🎯 Development Workflow

### Starting Development

1. **Quick Start**: `./start-all.bat` (Windows) or `./start-all.sh` (Linux/Mac)
2. **Mobile Testing**: Scan QR code with Expo Go
3. **Real Analysis**: Test mood detection with camera
4. **Music Playback**: Verify music generation and playback

### Development Tools

```bash
# Port management
npx kill-port 3001    # Face API
npx kill-port 8081    # Expo

# Network testing
node scripts/test-network.js
node scripts/find-ip.js

# Service testing
curl http://localhost:3001/health
```

### Code Quality

- **TypeScript** for type safety
- **ESLint** for code quality
- **Prettier** for formatting
- **Expo** best practices

## 🤝 Contributing

### Development Setup

1. **Fork** the repository
2. **Create feature branch**: `git checkout -b feature/amazing-feature`
3. **Follow setup instructions** above
4. **Test changes** with `./start-all.bat`
5. **Commit changes**: `git commit -m 'Add amazing feature'`
6. **Push to branch**: `git push origin feature/amazing-feature`
7. **Open Pull Request**

### Code Style

- Use **TypeScript** for all new code
- Follow **Expo** and **React Native** best practices
- Add **proper error handling** and logging
- Include **tests** for new features

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **face-api.js** for facial emotion recognition
- **Spotify** for music data and API
- **Supabase** for backend services
- **ngrok** for tunnel access
- **Expo** for cross-platform development
- **React Native** community for excellent tools

## 📞 Support

### Get Help

- **🐛 Issues**: [GitHub Issues](https://github.com/sandunMadhushan/mood-melodies-app/issues)
- **💬 Discussions**: [GitHub Discussions](https://github.com/sandunMadhushan/mood-melodies-app/discussions)
- **📚 Documentation**: [Development Guide](./docs/DEV-GUIDE.md)

### Quick Support Commands

```bash
# Health check all services
curl http://localhost:3001/health

# Restart everything
./start-all.bat  # or ./start-all.sh

# Clear Expo cache
npx expo start --clear

# Test network connectivity
node scripts/test-network.js
```

### Version

**Current Version**: 1.0.0  
**Last Updated**: August 30, 2025  
**Node.js**: 18+  
**Expo SDK**: 53  
**React Native**: Latest

---

_Transform your emotions into musical experiences_ 🎵✨

**🚀 Ready to start? Run `./start-all.bat` and scan the QR code!**
