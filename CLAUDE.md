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

This is a single-component React app built with Vite. All application logic lives in `src/App.jsx` — there are no sub-components, no routing, no state management library, and no backend.

**State** is managed entirely with `useState` in `App`:
- `transactions` — array of transaction objects (`{ id, description, amount, type, category, date }`)
- Form fields: `description`, `amount`, `type`, `category`
- Filter controls: `filterType`, `filterCategory`

**Known bug**: `amount` is stored as a string (from the input value), so `.reduce()` on it concatenates strings instead of summing numbers — totals and balance display incorrectly for the seed data and any added transactions.

**Seed data**: Transaction #4 ("Freelance Work") is typed as `"expense"` but categorized as `"salary"` — likely an intentional data error from the course.

**Styling**: Plain CSS in `src/App.css` with utility classes `income-amount`, `expense-amount`, `balance-amount`, and `delete-btn` (the delete button is styled but delete functionality is not implemented in the starter).
