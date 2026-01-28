# PalmPay Banking App with Paystack Integration

A banking application with real-time bank account verification using Paystack API.

## Features

- 💰 Balance management
- 💸 Money transfers with bank account verification
- 📊 Transaction history
- 🌓 Dark/Light mode
- ✅ Real-time account verification via Paystack
- 🏦 Support for all Paystack banks + Fintech banks (OPay, PalmPay, Kuda, MoniePoint, Carbon)
- 🔍 Automatic account name resolution for all banks

## Setup Instructions

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Paystack

1. Create a `.env` file in the root directory with your Paystack test secret key:

```env
PAYSTACK_SECRET_KEY=sk_test_de75561e917c46613b4c146af8514ac902c17d6a
PORT=3000
NODE_ENV=development
```

**Note:** The app uses a test Paystack secret key for account verification. For production, replace with your live key from [Paystack Dashboard](https://dashboard.paystack.com/#/settings/developer).

### 3. Start the Server

```bash
npm start
```

For development with auto-reload:

```bash
npm run dev
```

The app will be available at `http://localhost:3000`

## API Endpoints

### GET /api/paystack/banks
Fetches all Nigerian banks from Paystack.

**Response:**
```json
{
  "status": true,
  "message": "Banks fetched successfully",
  "data": [
    {
      "name": "Access Bank",
      "code": "044",
      "longcode": "044150149",
      "gateway": "emandate",
      "pay_with_bank": false,
      "active": true,
      "is_deleted": false,
      "country": "Nigeria",
      "currency": "NGN",
      "type": "nuban"
    }
  ]
}
```

### POST /api/paystack/verify
Verifies a bank account number for both Paystack banks and fintech banks.

**Request Body:**
```json
{
  "account_number": "0123456789",
  "bank_code": "044"
}
```

**Response (Paystack Bank):**
```json
{
  "status": true,
  "message": "Account resolved successfully",
  "data": {
    "account_number": "0123456789",
    "account_name": "JOHN DOE",
    "bank_id": 1,
    "is_fintech": false
  }
}
```

**Response (Fintech Bank):**
```json
{
  "status": true,
  "message": "Account resolved successfully (Fintech)",
  "data": {
    "account_number": "0123456789",
    "account_name": "ADE ADEBAYO",
    "bank_id": "999992",
    "bank_name": "OPay",
    "is_fintech": true
  }
}
```

**Supported Fintech Banks:**
- OPay (code: 999992)
- PalmPay (code: 999991)
- MoniePoint (code: 50515)
- Kuda Bank (code: 50211)
- Carbon (code: 50457)

## Project Structure

```
.
├── server.js                 # Express server
├── package.json              # Dependencies
├── .env                      # Environment variables (create this)
├── index.html               # Main app page
├── Transaction History.html # Transaction history page
└── src/
    └── routes/
        └── paystack.js      # Paystack API routes
```

## Usage

1. Click "To Bank" on the home page
2. Search and select a bank from the dropdown (all Paystack banks + fintech banks)
3. Enter the 10-digit account number
4. The account name will be **automatically verified and displayed** (no manual entry required)
5. Enter the amount and click "Transfer"

**Note:** Account verification works automatically for both regular banks (via Paystack API) and fintech banks (via Paystack API or fallback).

## Notes

- Account verification happens automatically when you enter 10 digits
- Transfers are disabled until account is successfully verified
- Uses Paystack test keys by default (use `sk_test_...`)
- **Test Mode Features:**
  - Fintech banks (OPay, PalmPay, Kuda, MoniePoint, Carbon) automatically return mock account names
  - If Paystack rate limit is reached, the app gracefully falls back to mock account names
  - All account names are automatically displayed (no manual entry required)
- For production, use live keys (`sk_live_...`) and replace mock functions with real API calls

## License

ISC

