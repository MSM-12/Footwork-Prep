# Footwork VC - Meeting Prep Agent

## Deploy to Netlify (5 minutes)

### Step 1: Push to GitHub
```bash
cd footwork-prep
git init
git add .
git commit -m "Footwork meeting prep agent"
```

Create a new repo on GitHub (private), then:
```bash
git remote add origin https://github.com/YOUR_USERNAME/footwork-prep.git
git branch -M main
git push -u origin main
```

### Step 2: Deploy on Netlify
1. Go to [app.netlify.com](https://app.netlify.com)
2. Click "Add new site" > "Import an existing project"
3. Connect your GitHub and select the `footwork-prep` repo
4. Build settings should auto-detect from `netlify.toml` - just click Deploy

### Step 3: Add your API key
1. In Netlify dashboard, go to **Site settings** > **Environment variables**
2. Add a new variable:
   - Key: `ANTHROPIC_API_KEY`
   - Value: your `sk-ant-api03-...` key
3. Redeploy the site (Deploys > Trigger deploy)

### Step 4: Custom domain (optional)
- Default URL will be something like `footwork-prep-abc123.netlify.app`
- You can change the subdomain in Site settings > Domain management
- e.g. `footwork-prep.netlify.app`

## Project structure
```
footwork-prep/
  index.html              <- The frontend (single file)
  netlify.toml             <- Netlify config
  netlify/functions/
    research.js            <- Serverless proxy (hides your API key)
```

## How it works
- Frontend sends requests to `/.netlify/functions/research`
- The serverless function adds your API key and forwards to Claude API
- Your key never touches the browser - completely server-side

## Cost
- Netlify free tier: 125K function invocations/month (more than enough)
- Claude API: each brief costs roughly $0.03-0.08 depending on web search usage
