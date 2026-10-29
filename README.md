# PennyWise — Personal Expense Manager

A dark, premium dashboard inspired by the supplied reference: compact left navigation, revenue-style overview, category donut, transaction table, date controls, soft borders and subtle motion.

## Features
- Register/login with bcrypt password hashing and JWT authentication
- MongoDB persistence through Mongoose
- Add, edit, delete and search income/expense transactions
- Category selection, date, payment method, notes and input validation
- Dashboard totals, savings rate, income-vs-expense chart, category breakdown and recent activity
- Monthly budget with progress/warning indicators
- CSV export for transactions
- Responsive layout, toast feedback, loading/empty states and subtle animations
- Demo mode when backend/MongoDB is not configured, using browser local storage. This is for UI demonstration only; use MongoDB for the assessed full-stack implementation.

## Requirements
- Node.js 18+
- MongoDB local installation or a MongoDB Atlas database

## Setup
1. Extract the ZIP and open the folder in VS Code.
2. In `server/`, copy `.env.example` to `.env`.
3. Set `MONGO_URI` to your MongoDB connection string and choose a strong `JWT_SECRET`.
4. From the project root run:
   ```bash
   npm run install:all
   npm run dev
   ```
5. Open `http://localhost:5173`. API runs at `http://localhost:5000`.

### MongoDB Atlas URI example
`mongodb+srv://YOUR_USER:YOUR_PASSWORD@YOUR_CLUSTER.mongodb.net/pennywise?retryWrites=true&w=majority`

Replace the placeholders with your own database credentials. Never commit `.env` to GitHub.

## Quick viva map
- **MongoDB connection:** `server/config.js`
- **Schemas / collections:** `server/models/User.js`, `server/models/Transaction.js`, `server/models/Budget.js`
- **Registration/login + password hashing/JWT:** `server/routes/auth.js`
- **CRUD and validation:** `server/routes/transactions.js`
- **Monthly budget:** `server/routes/budget.js`
- **Frontend API calls:** `client/src/api.js`
- **Main dashboard and UI:** `client/src/App.jsx`, `client/src/styles.css`

## Notes
- The application attempts to connect to MongoDB on server startup. If no MongoDB URI is configured, it clearly logs that the API is in demo/unconfigured mode; the frontend also includes local-storage demo mode so the interface can still be explored. For the rubric's full marks in integration, configure a real MongoDB URI and verify that the server logs `MongoDB connected`.
- Do not present demo/local-storage records as proof of database persistence. Add a record, restart the server, and inspect the MongoDB `pennywise` database to demonstrate persistence.
