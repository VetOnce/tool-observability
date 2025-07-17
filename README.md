# Observability Tool

Real-time monitoring system for Claude Code agents with Vue.js dashboard and WebSocket server.

**Repository**: https://github.com/VetOnce/tool-observability

This tool consists of two parts:
1. **Server**: WebSocket server that receives events from Claude Code hooks
2. **Client**: Vue.js dashboard for real-time visualization of agent activities

## Features

- 🔄 Real-time WebSocket streaming
- 📊 Event collection and storage
- 🔒 API key authentication (optional)
- 📈 Session tracking and analytics
- 🚀 High-performance with Bun runtime

## Requirements

- Bun 1.0+ or Node.js 18+
- SQLite3

## Installation

```bash
# Using Bun (recommended)
bun install

# Using npm
npm install
```

## Running Locally

```bash
# Development mode
bun run dev

# Production mode
bun start
```

The server will start on http://localhost:4000

## API Endpoints

- `GET /` - Health check
- `GET /health` - Server status
- `POST /events` - Submit events
- `WS /stream` - WebSocket connection for real-time updates

## Environment Variables

```env
# Server Configuration
PORT=4000
NODE_ENV=production

# Security
ALLOWED_ORIGINS=https://admin.shawandpartners.com,http://localhost:3000
API_KEY_REQUIRED=false
VALID_API_KEYS=key1,key2

# Database
DB_PATH=./data/observability.db

# Performance
MAX_EVENTS_PER_SESSION=10000
EVENT_RETENTION_DAYS=30
```

## Railway Deployment

This service is deployed on Railway:
- **Project**: organize-myself
- **Service Name**: tools (in Railway dashboard)
- **Builder**: Dockerfile
- **Runtime**: Bun

### Deployment Steps

1. Service is connected to `VetOnce/tool-observability` GitHub repository
2. Uses the included Dockerfile for Bun runtime
3. Automatic deployments on push to master
4. Environment variables configured in Railway dashboard

## Docker

```bash
# Build
docker build -t observability-server .

# Run
docker run -p 4000:4000 observability-server
```

## Integration with Manager

In your Manager app, set:
```env
NEXT_PUBLIC_OBSERVABILITY_SERVER_URL=https://your-domain.railway.app
NEXT_PUBLIC_OBSERVABILITY_WEBSOCKET_URL=wss://your-domain.railway.app
```

## Claude Code Hooks

The server receives events from Claude Code hooks installed in project directories. Events include:
- Tool usage (bash, read, write, etc.)
- Errors and exceptions
- Performance metrics
- Session information

## Database Schema

Events are stored in SQLite with:
- Session tracking
- Event timestamps
- Tool usage statistics
- Error logs
- Performance metrics

## Vue Client

The client directory contains a Vue.js dashboard for monitoring agent activities.

### Client Setup

```bash
cd client
npm install
npm run dev
```

### Client Configuration

Create a `.env` file in the client directory:

```env
# WebSocket URL for the observability server
VITE_WEBSOCKET_URL=wss://your-domain.railway.app/stream
VITE_MAX_EVENTS_TO_DISPLAY=100
```

### Client Features

- 🎯 Real-time event timeline with filtering
- 📊 Live activity pulse chart
- 🎨 Theme customization (dark/light/custom themes)
- 📱 Responsive design for mobile/desktop
- 🔍 Filter by source app, session ID, or event type
- 💬 Chat transcript viewer for agent conversations
- 🎯 Sticky scroll for live monitoring
