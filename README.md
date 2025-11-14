## 📑 QB: Budget Tracker

This is a full-stack budget tracking application built with a modern, high-performance stack. It allows users to manage expenses, income, debt, and track spending across defined budget periods.

### ✨ Tech Stack

This project leverages the following technologies for a fast, type-safe, and scalable experience:

- **Backend:**
  - **Framework:** [Hono RPC](https://hono.dev/) - A fast, lightweight, and modern web framework for the edge.
  - **Validation:** [Zod](https://zod.dev/) - TypeScript-first schema validation.
  - **ORM:** [Drizzle ORM](https://orm.drizzle.team/) - A modern, lightweight ORM for TypeScript.
- **Database:** [PostgreSQL](https://www.postgresql.org/)
- **Frontend:**
  - **Framework:** [React](https://react.dev/)
  - **Routing:** [TanStack Router](https://tanstack.com/router)
  - **State/Data Fetching:** [TanStack Query](https://tanstack.com/query) (React Query)
- **Runtime:** [Bun](https://bun.sh/) - An all-in-one JavaScript runtime, package manager, and bundler (used alongside Hono).

### 📐 Database Schema Overview

The application's data model is designed around tracking financial transactions, categorizing them, and managing debts within defined budget periods.

_(Based on the provided ERD)_

#### Core Tables

| Table Name           | Description                                                                                   | Key Fields                                                          | Relationships                                           |
| :------------------- | :-------------------------------------------------------------------------------------------- | :------------------------------------------------------------------ | :------------------------------------------------------ |
| **Transactions**     | Records individual financial movements (expense, income, transfer, etc.).                     | `id` (PK), `amount`, `description`, `is_recurring`, `next_due_date` | FK to `TransactionTypes`, `Categories`, `BudgetPeriods` |
| **Categories**       | General groups for organizing transactions (e.g., Food, Rent, Salary).                        | `id` (PK), `name`, `description`                                    | Many-to-Many with `TransactionTypes`                    |
| **TransactionTypes** | Defines the nature of a transaction (Expense, Income, Transfer, Debt Payment, Loan Received). | `id` (PK), `name`, `description`                                    | Many-to-Many with `Categories`                          |
| **BudgetPeriods**    | Defines timeframes for budget tracking (e.g., Monthly, Quarterly, specific projects).         | `id` (PK), `name`, `date`                                           | One-to-Many with `Transactions`                         |
| **Debts**            | Records loans or money owed/borrowed.                                                         | `id` (PK), `amount_borrowed`, `due_date`, `status`, `title`         | One-to-Many with `DebtPayments`                         |
| **DebtPayments**     | Records payments made towards a specific debt.                                                | `id` (PK), `amount_paid`, `date`                                    | FK to `Debts`, FK to `Transactions`                     |

> ℹ️ **Note:** The `transaction_type_id` in the `Transactions` table determines how the transaction is treated (e.g., an Expense reduces the budget balance).

---

### 🚀 Getting Started

Follow these steps to set up and run the project locally.

#### 1\. Prerequisites

- [Bun](https://bun.sh/docs/installation)
- A PostgreSQL database (e.g., a free tier instance from Neon.tech).

#### 2\. Environment Variables

Create a `.env` file in the root directory and add your database connection string:

```
DATABASE_URL="postgresql://[USER]:[PASSWORD]@[HOST]/[DB_NAME]?sslmode=require"
```

#### 3\. Installation

Install the project dependencies using Bun:

```bash
bun install
```

#### 4\. Database Setup

Run Drizzle migrations to set up the schema:

```bash
# Command placeholder: Replace with your actual Drizzle migration command
bun run db:migrate
```

#### 5\. Running the Application

Start the Hono backend and the React frontend (usually in separate terminal tabs):

```bash
# Start the Backend (Hono/Bun)
bun run start:backend

# Start the Frontend (React/Vite)
bun run start:frontend
```

The application should now be accessible, typically at `http://localhost:5173`.

---
