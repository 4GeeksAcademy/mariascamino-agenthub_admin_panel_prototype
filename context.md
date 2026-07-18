# AgentHub Project Context & Vision

## Product Overview
AgentHub is a Software-as-a-Service (SaaS) platform where companies can rent pre-configured intelligent AI agents. These agents can be equipped with specialized capabilities called **Skills** (such as web browsing, document reading, calendar management, database querying, etc.) and deployed to solve specific business automation tasks.

## Targeted Users
- **System Administrators**: Internal users responsible for platform operations, billing, monitoring system health, and managing tenant contracts.
- **Support Staff**: Team members who investigate agent failures, inspect logs, and manage user accounts.

## Tech Stack Constraints
- **HTML5 & Vanilla JavaScript**: The interface is built as a highly interactive single-page application (SPA) prototype inside a single `index.html` file (or multiple files linked natively) containing no external frameworks (no React, Vue, jQuery) and no build step.
- **Tailwind CSS via CDN**: Styling is controlled entirely via Tailwind utility classes. No custom CSS stylesheets or inline `style` attributes are permitted.
- **Tailwind Dark Mode**: Fully supported using Tailwind's `dark:` classes, toggled via a global theme controller which manages a `.dark` class on the `<html>` or `<body>` element.
- **Zero Backend**: All state and representation data are hardcoded within the frontend scripts, simulating functional modals, collapsibles, dropdowns, and dashboard metrics dynamically.