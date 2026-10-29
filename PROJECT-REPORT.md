
# PennyWise — Personal Expense Manager

## 1. Problem statement
Personal expenses often become difficult to understand when income, recurring costs and small day-to-day purchases are tracked in different places. PennyWise provides one dashboard for recording income and expenses, grouping spending into categories, setting a monthly limit and reviewing recent financial activity.

## 2. Objectives
- Build a responsive personal-finance dashboard with a consistent dark visual theme.
- Support account registration and login.
- Validate transaction fields before accepting data.
- Persist users, transactions and budgets in MongoDB.
- Provide create, read, update and delete operations for transactions.
- Summarize income, expenses, net cash flow and category-level spending.
- Allow CSV export and show budget-use feedback.

## 3. Technology stack
- Front end: React, JavaScript, CSS, Vite
- Back end: Node.js, Express
- Database: MongoDB with Mongoose
- Authentication: bcryptjs password hashing and JSON Web Tokens
- Charts: Recharts

## 4. Functional modules
1. **Authentication:** registration validates name, email and password; passwords are hashed before storage. Login checks the submitted password and returns a signed JWT.
2. **Transactions:** a signed-in user can add, view, edit, search/filter and delete their own income/expense records.
3. **Dashboard:** calculates monthly income, expense totals, net cash flow, savings rate and category totals from transaction records.
4. **Budget guardrail:** stores a budget per user and month, calculates usage and shows remaining budget or an overspending warning.
5. **CSV report:** exports the visible month's matching transactions to a CSV file.

## 5. Database design
### User
| Field | Purpose |
|---|---|
| `_id` | MongoDB primary identifier |
| `name` | Display name |
| `email` | Unique login email |
| `password` | bcrypt password hash, never plain text |
| `createdAt`, `updatedAt` | Audit timestamps |

### Transaction
| Field | Purpose |
|---|---|
| `_id` | Transaction identifier |
| `user` | Reference to the owning User |
| `type` | `income` or `expense` |
| `title` | Short transaction description |
| `amount` | Positive numeric amount |
| `category` | Income/expense category |
| `date` | Transaction date |
| `method` | UPI, Card, Cash, Bank transfer or Other |
| `note` | Optional note |
| `createdAt`, `updatedAt` | Audit timestamps |

### Budget
| Field | Purpose |
|---|---|
| `_id` | Budget identifier |
| `user` | Reference to the owning User |
| `month` | Month in `YYYY-MM` format |
| `limit` | Positive monthly spending limit |

## 6. API endpoints
| Method | Endpoint | Function |
|---|---|---|
| POST | `/api/auth/register` | Register a user |
| POST | `/api/auth/login` | Authenticate a user |
| GET | `/api/health` | API and MongoDB connection status |
| GET | `/api/transactions` | List signed-in user's transactions; supports month/type/search query parameters |
| POST | `/api/transactions` | Create transaction |
| PUT | `/api/transactions/:id` | Update owned transaction |
| DELETE | `/api/transactions/:id` | Delete owned transaction |
| GET | `/api/budget/:month` | Read monthly budget |
| PUT | `/api/budget/:month` | Create/update monthly budget |

## 7. Input validation and security
- Required fields are checked on both the client and server.
- Email format and password minimum length are validated during registration.
- Passwords are hashed using bcrypt with 12 salt rounds.
- JWT-protected endpoints require a valid bearer token.
- Transaction queries and updates are scoped to the authenticated user.
- Amounts, transaction type, category, payment method, date, title and note length are validated.
- MongoDB credentials and JWT secret belong in `server/.env`, which is excluded from Git.

## 8. Rubric alignment
| Criterion | Evidence |
|---|---|
| Website design | Responsive dashboard, navigation, charts, category panel, transaction list, dialogs, hover states and animations in `client/src/styles.css` and `App.jsx` |
| Input validation | Client form constraints plus server-side validation in `server/routes/auth.js` and `server/routes/transactions.js` |
| Front-end/back-end integration | `client/src/api.js` calls Express endpoints; Mongoose models persist data in MongoDB |
| Presentation/viva | This report documents modules, schema, API routes and file locations |
| GitHub repository/report | This report and README are included. Create a repository under your own GitHub account and push the project after adding your own `.env` locally; do not upload credentials. |

## 9. Testing checklist
- [ ] Start MongoDB or configure MongoDB Atlas.
- [ ] Verify `GET http://localhost:5000/api/health` reports `database: connected`.
- [ ] Register a new account; verify a User record exists and password is hashed.
- [ ] Log in with correct and incorrect credentials.
- [ ] Add an income and an expense; confirm they appear in the dashboard and database.
- [ ] Try a blank title, invalid amount and invalid date; confirm validation blocks them.
- [ ] Edit and delete a transaction; confirm the database changes.
- [ ] Set a monthly budget and verify the progress indicator changes.
- [ ] Export a CSV and open it to confirm rows and headers.
- [ ] Restart the app and confirm database records remain available.

## 10. Conclusion
PennyWise demonstrates a full-stack CRUD application with authentication, server-side validation, MongoDB persistence, calculated dashboard summaries and a monthly budget feature. Before submission, complete the testing checklist using your own MongoDB connection and capture screenshots of the running application and database collections.
