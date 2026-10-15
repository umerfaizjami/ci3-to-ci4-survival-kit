# 🛠️ CI3 to CI4 Survival Kit

> **Stop staring at your legacy CodeIgniter 3 codebase in despair. Start migrating with confidence.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![CI Version](https://img.shields.io/badge/CodeIgniter_3_%E2%86%92_4-migration-orange.svg)](#)

---

## 😰 The Problem

CodeIgniter 3 served us well — but it has reached end-of-life. CodeIgniter 4 is a **complete rewrite**: new folder structure, new namespace conventions, a revamped ORM, middleware instead of hooks, PSR-4 autoloading, and an entirely different approach to almost everything.

**There is no automated upgrade path. The official migration guide is minimal. And your 200,000-line CI3 monolith isn't going to refactor itself.**

If you've ever found yourself:

- 🔍 Searching *"CI3 equivalent in CI4"* for the hundredth time
- 😤 Debugging why `$this->load->model()` doesn't exist anymore
- 🤯 Trying to remember whether it's `$this->input->post()` or `$this->request->getPost()`
- 📁 Staring at CI4's folder structure wondering where your code is supposed to live
- ⏳ Estimating a migration timeline for your team and having *no idea* where to start

**This repo is for you.**

---

## 📦 What's Inside

This survival kit is a curated, battle-tested collection of resources organized to guide you through every stage of migration — whether you're converting a small side project or a massive enterprise application.

### 📋 Cheat Sheets

Side-by-side reference tables so you never have to guess the CI4 equivalent again.

| Cheat Sheet | Description |
|---|---|
| [`cheatsheets/routing.md`](cheatsheets/routing.md) | `$route['...']` → `$routes->get(...)` and beyond |
| [`cheatsheets/models.md`](cheatsheets/models.md) | CI3 models → CI4 `CodeIgniter\Model` with entities |
| [`cheatsheets/controllers.md`](cheatsheets/controllers.md) | Loading views, helpers, libraries — the new way |
| [`cheatsheets/database.md`](cheatsheets/database.md) | Query Builder changes, `$this->db` → `db_connect()` |
| [`cheatsheets/views.md`](cheatsheets/views.md) | View rendering, layouts, sections, and view cells |
| [`cheatsheets/input-request.md`](cheatsheets/input-request.md) | `$this->input` → `$this->request` full mapping |
| [`cheatsheets/sessions.md`](cheatsheets/sessions.md) | Session library changes and gotchas |
| [`cheatsheets/helpers.md`](cheatsheets/helpers.md) | Which helpers survived, which were removed, what changed |
| [`cheatsheets/config.md`](cheatsheets/config.md) | `$this->config->item()` → Config classes and `.env` |
| [`cheatsheets/hooks-to-events.md`](cheatsheets/hooks-to-events.md) | Hooks & filters → CI4 Events and Controller Filters |
| [`cheatsheets/libraries.md`](cheatsheets/libraries.md) | Custom library migration & service container patterns |
| [`cheatsheets/uri-urls.md`](cheatsheets/uri-urls.md) | URL helper and URI segment changes |

> 💡 **Each cheat sheet follows a consistent format:** CI3 code → CI4 equivalent → explanation → edge cases.

---

### 🔎 VS Code Regex Recipes

Automate the tedious parts. These are **tested find-and-replace regex patterns** you can run directly in VS Code (or any editor that supports regex search) to bulk-transform common CI3 patterns.

📂 **Located in [`regex-recipes/`](regex-recipes/)**
