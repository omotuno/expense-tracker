# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies (required before first run)
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # run ESLint
npm run preview  # preview production build locally
```

There are no tests in this project.

## Architecture

React app built with Vite, split into four components. No routing, no state management library, no backend.

**Component structure:**
- `App.jsx` — holds `transactions` state and passes it down; the only place `setTransactions` is called
- `Summary.jsx` — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally
- `TransactionForm.jsx` — owns its own form state (`description`, `amount`, `type`, `category`); calls `onAdd(transaction)` prop on submit
- `TransactionList.jsx` — receives `transactions`, owns filter state (`filterType`, `filterCategory`) internally

**Transaction shape**: `{ id, description, amount (number), type ("income"|"expense"), category, date (YYYY-MM-DD) }`

**Shared constants**: `categories` array is duplicated in `TransactionForm` and `TransactionList` — no shared constants file yet.

**Seed data**: Transaction #4 ("Freelance Work") is typed as `"expense"` but categorized as `"salary"`.

**Styling**: Plain CSS in `src/App.css` with utility classes `income-amount`, `expense-amount`, `balance-amount`, and `delete-btn` (the delete button is styled but delete functionality is not yet implemented).
