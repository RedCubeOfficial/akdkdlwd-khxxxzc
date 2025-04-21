# Discord Download Manager Bot

A comprehensive Discord bot for managing downloads with role-based access control and premium features. Designed to handle 10,000+ items with efficient search and database management.

## Features

- Multiple download links with role-based access
- Standard and premium downloads
- Customizable daily download limits per role
- Interactive search panel
- Time-limited premium subscription system
- Advanced item management
- Customizable UI elements
- MongoDB and SQLite database support for efficient storage of 10,000+ items
- Automatic premium role expiration
- Premium-only download restrictions

## Local Setup

1. Install dependencies:
```bash
npm install
```

2. Copy `.env.example` to `.env` and fill in your bot token and configuration:
```bash
cp .env.example .env
```

3. Start the bot:
```bash
npm start
```

## Deployment to Render

### Prerequisites
- GitHub account
- Render account (sign up at https://render.com)
- MongoDB Atlas account (for database)

### Step 1: Push Your Code to GitHub
1. Create a new GitHub repository
2. Push your bot code to the repository

### Step 2: Set Up MongoDB Atlas
1. Create a free MongoDB Atlas account
2. Create a new cluster
3. Create a database user with read/write permissions
4. Get your MongoDB connection string

### Step 3: Deploy to Render
1. Log in to your Render account
2. Click on "New +" and select "Web Service"
3. Connect your GitHub repository
4. Configure the service:
   - **Name**: discord-download-manager (or your preferred name)
   - **Environment**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `node src/index.js`
5. Add environment variables:
   - `TOKEN`: Your Discord bot token
   - `USE_MONGO`: true
   - `USE_SQLITE`: true
   - `MONGO_URI`: Your MongoDB Atlas connection string
   - `DB_NAME`: searchbot
6. Select the free plan and click "Create Web Service"

### Step 4: Keep Your Bot Alive
To prevent your bot from sleeping on Render's free tier:
1. Set up a monitoring service like UptimeRobot to ping your bot's URL every 5 minutes
2. The keep-alive server we added will respond to these pings

### Important Notes for Render Free Tier
- Your bot may experience some downtime on the free tier
- The bot will go to sleep after 15 minutes of inactivity
- Use the keep-alive server and UptimeRobot to minimize downtime
- Consider upgrading to a paid plan ($7/month) for 24/7 uptime

## Commands

### General Commands
- `/panel` - Show the main search panel
- `/search` - Search for items directly
- `/list` - List all available items
- `/help` - Show all available commands

### Item Management
- `/add-item` - Add new items
- `/edit-item` - Edit existing items
- `/delete-item` - Delete an item

### Premium System
- `/activate {user} {role} {days}` - Activate premium for a user for a specified number of days
- `/premium-status [user]` - Check premium status for yourself or another user
- `/premium-roles list` - List all premium roles
- `/premium-roles add {role} {limit}` - Add a role as premium
- `/premium-roles update {role} {limit}` - Update a premium role's settings
- `/premium-roles remove {role}` - Remove a role from premium

### Admin Commands
- `/panel-edit` - Edit panel settings
- `/d-msg` - Set download message
- `/reload` - Reload bot data and sync commands
- `/download-stats` - View download statistics

## Data Storage

The bot uses SQLite as the primary database with JSON files as fallback:

### SQLite Database
- `data/searchbot.sqlite` - Main database for storing items and search indexes

### JSON Files
- `items.json` - Backup storage for items (used as fallback)
- `roles.json` - Stores premium role configurations
- `settings.json` - Stores bot settings
- `download_counts.json` - Tracks user download counts
- `premium_users.json` - Stores premium user subscriptions and expiration dates

## Database Configuration

The bot supports multiple database backends that can be configured in the `.env` file:

```
# Use SQLite (recommended for most deployments)
USE_SQLITE=true

# Use MongoDB (optional for larger deployments)
USE_MONGO=false
MONGO_URI=mongodb://localhost:27017
DB_NAME=searchbot
```
y
