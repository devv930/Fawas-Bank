# Setup Instructions for Paystack Integration

## Important: Server Setup Required

Your banking app now requires a **backend Express server** to handle Paystack API calls. You cannot run it directly from Live Server alone.

## Quick Start

### Step 1: Install Dependencies

Open your terminal in the project folder and run:

```bash
npm install
```

### Step 2: Configure Paystack API Key

1. Create a `.env` file in the root directory (same folder as `package.json`)
2. Get your Paystack Secret Key from: https://dashboard.paystack.com/#/settings/developer
3. Add to `.env`:

```env
PAYSTACK_SECRET_KEY=sk_test_your_secret_key_here
PORT=3000
NODE_ENV=development
```

### Step 3: Start the Express Server

```bash
npm start
```

You should see:
```
Server running on http://localhost:3000
Make sure to set PAYSTACK_SECRET_KEY in your .env file
```

### Step 4: Access the App

**Important:** Open your browser and go to:
```
http://localhost:3000
```

**Do NOT use Live Server** (port 5502). The Express server serves your HTML files AND handles the API routes.

## Troubleshooting

### Error: "Failed to load resource: 404"

**Problem:** You're accessing the app through Live Server instead of the Express server.

**Solution:** 
1. Make sure the Express server is running (`npm start`)
2. Access the app at `http://localhost:3000` (not through Live Server)

### Error: "Paystack secret key not configured"

**Problem:** The `.env` file is missing or doesn't have the correct key.

**Solution:**
1. Create a `.env` file in the root directory
2. Add: `PAYSTACK_SECRET_KEY=sk_test_your_key_here`
3. Restart the server

### Error: "Cannot find module"

**Problem:** Dependencies not installed.

**Solution:** Run `npm install`

## Development Mode

For auto-reload during development:

```bash
npm run dev
```

This uses `nodemon` to automatically restart the server when you make changes.

## Production

For production, use your live Paystack keys:

```env
PAYSTACK_SECRET_KEY=sk_live_your_live_key_here
NODE_ENV=production
```

## File Structure

```
Practice 6month/
├── server.js              # Express server
├── package.json           # Dependencies
├── .env                   # API keys (create this)
├── index.html            # Main app
├── src/
│   └── routes/
│       └── paystack.js   # Paystack API routes
└── ...
```

## Testing

1. Start the server: `npm start`
2. Open: `http://localhost:3000`
3. Click "To Bank"
4. Select a bank from dropdown
5. Enter a 10-digit account number
6. Account name should auto-verify

