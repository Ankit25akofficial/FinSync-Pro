# FinSync Pro - Personal Finance Manager & Budget Tracker

A complete, production-ready Personal Finance Manager & Budget Tracker web application built with React, Node.js, Express, MongoDB, and Clerk Authentication.

## 🚀 Features

### Core Features
- ✅ **Authentication** - Secure sign up, sign in, and logout using Clerk
- ✅ **Transaction Management** - Add, edit, delete income and expenses with categories
- ✅ **Budget Tracking** - Set monthly budgets with real-time progress tracking and alerts
- ✅ **Financial Analytics** - Income vs expenses, spending by category, monthly trends
- ✅ **Smart Filters** - Filter by date range, category, type, and search by keyword
- ✅ **Goal-Based Savings** - Create and track financial goals with AI suggestions
- ✅ **Investment Tracker** - Track stocks, mutual funds, SIPs, and calculate profit/loss
- ✅ **Real-Time Updates** - Socket.io for live transaction and budget updates
- ✅ **Export Reports** - Download transactions as PDF, Excel, or CSV

### Advanced Features
- ✅ **OCR Bank Statement Scanner** - Upload PDF/image to extract transactions
- ✅ **AI Chatbot** - Personal finance assistant for queries
- ✅ **AI Auto-Categorization** - Automatically categorize expenses
- ✅ **Admin Dashboard** - Fraud detection and user management
- ✅ **Glassmorphism UI** - Beautiful modern UI with animations
- ✅ **Dark Mode** - Full dark theme support
- ✅ **Responsive Design** - Mobile-friendly interface

## 📋 Prerequisites

- Node.js (v18 or higher)
- MongoDB Atlas account or local MongoDB
- Clerk account for authentication
- npm or yarn

## 🛠️ Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd FNS
```

### 2. Backend Setup

```bash
cd server
npm install
```

Create a `.env` file in the `server` directory:

```env
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/finsync-pro
CLERK_SECRET_KEY=sk_test_your_clerk_secret_key
CLERK_PUBLISHABLE_KEY=pk_test_your_clerk_publishable_key
JWT_SECRET=your_jwt_secret_key_here
NODE_ENV=development
OPENAI_API_KEY=your_openai_api_key_optional
CURRENCY_API_KEY=your_currency_api_key_optional
CLIENT_URL=http://localhost:5173
```

Create the `uploads` directory:

```bash
mkdir uploads
```

### 3. Frontend Setup

```bash
cd ../client
npm install
```

Create a `.env` file in the `client` directory:

```env
VITE_API_URL=http://localhost:5000/api
VITE_CLERK_PUBLISHABLE_KEY=pk_test_your_clerk_publishable_key
```

## 🚀 Running the Application

### Start Backend Server

```bash
cd server
npm run dev
```

The server will run on `http://localhost:5000`

### Start Frontend Development Server

```bash
cd client
npm run dev
```

The frontend will run on `http://localhost:5173`

## 📁 Project Structure

```
FNS/
├── server/                 # Backend (Node.js + Express)
│   ├── config/            # Configuration files
│   ├── controllers/       # Route controllers
│   ├── middleware/        # Custom middleware
│   ├── models/            # MongoDB models
│   ├── routes/            # API routes
│   ├── server.js          # Main server file
│   └── package.json
│
├── client/                # Frontend (React + Vite)
│   ├── src/
│   │   ├── components/   # React components
│   │   ├── pages/        # Page components
│   │   ├── store/        # Redux store
│   │   ├── utils/         # Utility functions
│   │   ├── App.jsx        # Main app component
│   │   └── main.jsx       # Entry point
│   └── package.json
│
└── README.md
```

## 🔌 API Documentation

### Authentication Routes

#### `GET /api/auth/me`
Get current user profile
- **Auth Required**: Yes
- **Response**: User object

#### `PUT /api/auth/me`
Update user preferences
- **Auth Required**: Yes
- **Body**: `{ currency, language, preferences }`

### Transaction Routes

#### `GET /api/transactions`
Get all transactions with filters
- **Auth Required**: Yes
- **Query Params**: `type`, `category`, `startDate`, `endDate`, `search`, `page`, `limit`
- **Response**: Array of transactions with pagination

#### `GET /api/transactions/:id`
Get single transaction
- **Auth Required**: Yes
- **Response**: Transaction object

#### `POST /api/transactions`
Create new transaction
- **Auth Required**: Yes
- **Body**: `{ type, amount, category, description, date, paymentMethod, notes }`
- **Response**: Created transaction

#### `PUT /api/transactions/:id`
Update transaction
- **Auth Required**: Yes
- **Body**: Same as POST
- **Response**: Updated transaction

#### `DELETE /api/transactions/:id`
Delete transaction
- **Auth Required**: Yes
- **Response**: Success message

### Budget Routes

#### `GET /api/budgets`
Get all budgets
- **Auth Required**: Yes
- **Query Params**: `month`, `year`
- **Response**: Array of budgets

#### `POST /api/budgets`
Create or update budget
- **Auth Required**: Yes
- **Body**: `{ category, monthlyLimit, month, year }`
- **Response**: Budget object

#### `PUT /api/budgets/:id`
Update budget
- **Auth Required**: Yes
- **Body**: Same as POST
- **Response**: Updated budget

#### `DELETE /api/budgets/:id`
Delete budget
- **Auth Required**: Yes
- **Response**: Success message

### Analytics Routes

#### `GET /api/analytics/dashboard-summary`
Get dashboard summary
- **Auth Required**: Yes
- **Response**: Summary object with wallet balance, income, expenses, etc.

#### `GET /api/analytics/income-vs-expenses`
Get income vs expenses data
- **Auth Required**: Yes
- **Query Params**: `startDate`, `endDate`
- **Response**: `{ income, expenses, savings, percentage }`

#### `GET /api/analytics/spending-by-category`
Get spending by category (pie chart data)
- **Auth Required**: Yes
- **Query Params**: `startDate`, `endDate`
- **Response**: Array of `{ category, amount, percentage }`

#### `GET /api/analytics/monthly-trends`
Get monthly trends
- **Auth Required**: Yes
- **Query Params**: `months` (default: 6)
- **Response**: Array of monthly data

### Goal Routes

#### `GET /api/goals`
Get all goals
- **Auth Required**: Yes
- **Query Params**: `status`
- **Response**: Array of goals

#### `POST /api/goals`
Create goal
- **Auth Required**: Yes
- **Body**: `{ title, description, targetAmount, currentAmount, targetDate }`
- **Response**: Created goal with AI suggestions

#### `PUT /api/goals/:id`
Update goal
- **Auth Required**: Yes
- **Body**: Same as POST
- **Response**: Updated goal

#### `DELETE /api/goals/:id`
Delete goal
- **Auth Required**: Yes
- **Response**: Success message

### Investment Routes

#### `GET /api/investments`
Get all investments
- **Auth Required**: Yes
- **Query Params**: `type`
- **Response**: Array of investments with summary

#### `POST /api/investments`
Create investment
- **Auth Required**: Yes
- **Body**: `{ type, name, symbol, investedAmount, purchaseDate, purchasePrice, quantity }`
- **Response**: Created investment

#### `PUT /api/investments/:id`
Update investment
- **Auth Required**: Yes
- **Body**: Same as POST
- **Response**: Updated investment

#### `DELETE /api/investments/:id`
Delete investment
- **Auth Required**: Yes
- **Response**: Success message

### OCR Routes

#### `POST /api/ocr/image`
Process image OCR
- **Auth Required**: Yes
- **Body**: FormData with `file` (image)
- **Response**: `{ extractedText, transactions, count }`

#### `POST /api/ocr/pdf`
Process PDF OCR
- **Auth Required**: Yes
- **Body**: FormData with `file` (PDF)
- **Response**: `{ extractedText, transactions, count }`

#### `POST /api/ocr/import`
Import transactions from OCR results
- **Auth Required**: Yes
- **Body**: `{ transactions: [...] }`
- **Response**: Created transactions

### AI Routes

#### `POST /api/ai/chat`
Chat with AI assistant
- **Auth Required**: Yes
- **Body**: `{ message }`
- **Response**: `{ response, context }`

#### `POST /api/ai/categorize`
Auto-categorize expense
- **Auth Required**: Yes
- **Body**: `{ description }`
- **Response**: `{ category, confidence }`

#### `GET /api/ai/suggestions`
Get spending suggestions
- **Auth Required**: Yes
- **Response**: Array of suggestions

### Export Routes

#### `GET /api/export/excel`
Export transactions as Excel
- **Auth Required**: Yes
- **Query Params**: `startDate`, `endDate`
- **Response**: Excel file

#### `GET /api/export/csv`
Export transactions as CSV
- **Auth Required**: Yes
- **Query Params**: `startDate`, `endDate`
- **Response**: CSV file

#### `GET /api/export/pdf`
Export transactions as PDF
- **Auth Required**: Yes
- **Query Params**: `startDate`, `endDate`
- **Response**: PDF file

### Admin Routes

#### `GET /api/admin/users`
Get all users (Admin only)
- **Auth Required**: Yes (Admin)
- **Response**: Array of users

#### `GET /api/admin/fraud-alerts`
Get fraud alerts (Admin only)
- **Auth Required**: Yes (Admin)
- **Query Params**: `status`
- **Response**: Array of alerts

#### `PUT /api/admin/fraud-alerts/:id`
Update fraud alert status (Admin only)
- **Auth Required**: Yes (Admin)
- **Body**: `{ status }`
- **Response**: Updated alert

#### `GET /api/admin/stats`
Get system statistics (Admin only)
- **Auth Required**: Yes (Admin)
- **Response**: System stats

## 🎨 Tech Stack

### Frontend
- **React 18** - UI library
- **Vite** - Build tool
- **TailwindCSS** - Styling
- **Redux Toolkit** - State management
- **React Router** - Routing
- **Framer Motion** - Animations
- **Recharts** - Data visualization
- **Clerk** - Authentication
- **Socket.io Client** - Real-time updates
- **Axios** - HTTP client

### Backend
- **Node.js** - Runtime
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **Socket.io** - Real-time communication
- **Clerk** - Authentication
- **Express Validator** - Validation
- **Multer** - File uploads
- **Tesseract.js** - OCR
- **ExcelJS** - Excel export
- **PDFKit** - PDF export

## 🔐 Environment Variables

### Server (.env)
```
PORT=5000
MONGODB_URI=your_mongodb_connection_string
CLERK_SECRET_KEY=your_clerk_secret_key
CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
JWT_SECRET=your_jwt_secret
NODE_ENV=development
OPENAI_API_KEY=your_openai_key (optional)
CLIENT_URL=http://localhost:5173
```

### Client (.env)
```
VITE_API_URL=http://localhost:5000/api
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
```

## 📱 Deployment

### Backend (Render/Railway)
1. Connect your GitHub repository
2. Set environment variables
3. Build command: `npm install`
4. Start command: `npm start`
5. Set MongoDB Atlas connection string

### Frontend (Vercel)
1. Connect your GitHub repository
2. Set root directory to `client`
3. Build command: `npm run build`
4. Output directory: `dist`
5. Set environment variables

## 🧪 Testing

```bash
# Backend
cd server
npm test

# Frontend
cd client
npm test
```

## 📝 License

This project is licensed under the MIT License.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Support

For support, email support@finsyncpro.com or create an issue in the repository.

## 🎯 Future Enhancements

- [ ] PWA support for mobile app
- [ ] Multi-currency support
- [ ] Family mode with shared budgets
- [ ] EMI calculator
- [ ] Tax estimator
- [ ] Recurring transaction automation
- [ ] Email notifications
- [ ] Mobile app (React Native)

---

## To run the code just write this 
```
cd C:\FNS\server; Start-Process powershell -ArgumentList "-NoExit", "-Command", "npm run dev" -WindowStyle Minimized
```
```
cd C:\FNS\client; Start-Process powershell -ArgumentList "-NoExit", "-Command", "npm run dev" -WindowStyle Minimized
```
**Built with using modern web technologies** 
**~made by Ankit**

