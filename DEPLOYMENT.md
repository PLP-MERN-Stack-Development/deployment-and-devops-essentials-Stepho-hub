# Deployment Guide

This guide provides step-by-step instructions for deploying the Real-Time Chat Application to production.

## Backend Deployment (Render)

1. **Create a Render Account**: Go to [render.com](https://render.com) and sign up for an account.

2. **Connect GitHub Repository**:
   - In your Render dashboard, click "New" → "Web Service"
   - Connect your GitHub account and select this repository

3. **Configure the Service**:
   - **Name**: real-time-chat-backend
   - **Runtime**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`

4. **Environment Variables**:
   - `JWT_SECRET`: Set a secure JWT secret key
   - `NODE_ENV`: production
   - `PORT`: (Render sets this automatically)

5. **Deploy**: Click "Create Web Service" to deploy

## Frontend Deployment (Vercel)

1. **Create a Vercel Account**: Go to [vercel.com](https://vercel.com) and sign up.

2. **Deploy from GitHub**:
   - Click "New Project" in your Vercel dashboard
   - Import your GitHub repository
   - Vercel will automatically detect it as a Vite project

3. **Configure Build Settings**:
   - **Framework Preset**: Vite (should auto-detect)
   - **Root Directory**: ./
   - **Build Command**: `npm run build` (should auto-detect)
   - **Output Directory**: dist (should auto-detect)
   - The `_redirects` file in `public/` will handle SPA routing

4. **Environment Variables**:
   - `VITE_SOCKET_URL`: Set to your Render backend URL (e.g., `https://your-backend.onrender.com`)

5. **Deploy**: Click "Deploy"

## Post-Deployment Configuration

1. **Update CORS in Backend**: After deploying the frontend, update the backend's CORS settings to allow requests from your Vercel domain.

2. **Update Frontend Environment**: Ensure the `VITE_SOCKET_URL` in Vercel points to your Render backend URL.

3. **Test the Application**: Visit your deployed frontend URL and test the chat functionality.

## Troubleshooting

- **CORS Issues**: Make sure the backend allows requests from your frontend domain
- **WebSocket Connection**: Ensure the frontend's `VITE_SOCKET_URL` matches your backend URL
- **Build Failures**: Check that all dependencies are properly listed in package.json