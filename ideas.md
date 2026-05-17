# DSOC Feature 2026 Ideas

This file captures the DSOC feature proposals for VoiceyBill and organizes them into implementation-ready themes.

Program link: https://www.devweekends.com/dsoc/

## Project Overview

- Project: VoiceyBill - Personal Financial Platform
- Website: voiceybill.com
- GitHub: github.com/voiceyBill
- Total features proposed: 7
- Tech stack: TypeScript, React 19, React Native (Expo), Express, MongoDB, Open AI

## About VoiceyBill

VoiceyBill is an open-source personal finance platform that lets users track income and expenses using natural voice input. Users can speak in Hindi, Urdu, or English, and the app creates the expense entry automatically. The platform also includes AI receipt scanning, analytics charts, and scheduled email reports across a web app and a React Native mobile app.

## Feature Index

| # | Feature | Category | Difficulty | Repo |
| --- | --- | --- | --- | --- |
| 1 | Budget Management and Category-Based Spending Limits | Core Feature | Intermediate | voiceyBill-server + voiceyBill-web |
| 2 | Smart Recurring Expense Detection | Intelligence | Intermediate | voiceyBill-server + voiceyBill-web |
| 3 | Offline Voice Queue - Record Now, Process When Online | Reliability | Intermediate | voiceyBill-web + voiceyBill-App |
| 4 | Multi-Currency Support | Internationalisation | Intermediate | voiceyBill-server + voiceyBill-web |
| 5 | Multi-Language UI Support with Urdu | Internationalisation | Intermediate | voiceyBill-web + voiceyBill-App |
| 6 | Conversational Expense Q&A | AI Feature | Intermediate | voiceyBill-server + voiceyBill-web |
| 7 | Voice-Powered Group Expense Splitting | Social Finance | Intermediate | voiceyBill-server + voiceyBill-web + voiceyBill-App |

## 1. Budget Management and Category-Based Spending Limits

Category: Core Feature | Difficulty: Intermediate | Repo: voiceyBill-server + voiceyBill-web

### Problem Statement

VoiceyBill lets users track income and expenses but does not yet provide a way to plan or control spending through budgets. Users need category-wise spending limits, remaining budget indicators, planned versus actual comparisons, and alerts when they approach a limit. Without that, it is difficult to maintain spending discipline.

### Proposed Solution

Introduce a Budget Management module that lets users create and manage budgets for different spending categories with automatic expense integration, visual progress tracking, and overspending alerts.

### Core Functionality

1. Create Budgets - Users can create monthly, weekly, yearly, or custom budgets and allocate amounts to categories.
2. Budget Tracking - For every category the system displays allocated budget, amount spent, remaining amount, and percentage used.
3. Automatic Expense Integration - Expenses update the associated budget and category usage in real time.
4. Overspending Alerts - Users are notified when spending reaches a configurable threshold such as 80 percent of budget and again when the limit is exceeded.
5. Dashboard and Visualisation - Add progress bars, pie charts, monthly budget reports, spending trends, and remaining budget indicators.
6. Recurring Budgets - Budgets automatically reset on a monthly, weekly, or yearly basis.

### Acceptance Criteria

- Users can create, edit, and delete budgets
- Users can create category-based budgets with amounts
- Users can set budget periods: monthly, weekly, yearly, or custom
- Expenses automatically update budget usage
- Users can view total allocated budget, total spent, remaining balance, and usage percentage
- Budget progress indicators and charts display correctly
- Users receive alerts when budget usage reaches the configured threshold
- Users receive alerts when budget limits are exceeded
- Recurring budgets automatically reset based on the selected period
- Users can create, edit, and delete custom categories
- Budget data persists correctly after app restart or refresh
- No regressions to existing expense and income tracking features
- Documentation and UI labels are updated

## 2. Smart Recurring Expense Detection

Category: Intelligence | Difficulty: Intermediate | Repo: voiceyBill-server + voiceyBill-web

### Problem Statement

VoiceyBill already has a recurringInterval field on transactions, but it is entirely manual. Users must remember to mark recurring transactions themselves and usually do not. Subscriptions like Netflix, Spotify, gym fees, and rent appear as separate one-off entries every month. Users have no consolidated view of fixed monthly obligations, no early warning before a recurring charge hits, and no way to see how much of the budget is already pre-committed.

### Proposed Solution

Introduce a Recurring Detection Engine that watches transaction history in the background and automatically identifies repeating patterns, then surfaces them to the user for confirmation.

### Core Functionality

1. Pattern Detection - Group transactions by merchant name using fuzzy matching, similar amount within a five percent tolerance, and consistent date intervals for weekly, bi-weekly, monthly, or yearly patterns. When a group has three or more matching entries with a consistent interval it is flagged as a recurring suggestion.
2. User Confirmation Flow - Show merchant, amount, frequency, confidence, and next expected date.
3. Monthly Commitments Widget - Show total fixed monthly spend, each item with next expected date, and how much of the monthly budget is already committed.
4. Auto-Entry Generation - After confirmation, automatically create the next expected entry when the date arrives.
5. Pre-Charge Alerts - Notify users a configurable number of days before a recurring charge is expected, with three days as the default.
6. Analytics Separation - Clearly separate recurring and variable spend in category breakdown and monthly trend views.

### Acceptance Criteria

- System detects transactions with the same merchant, similar amount, and a consistent interval
- Fuzzy merchant name matching works correctly
- Suggestion cards are displayed on the dashboard
- User can confirm or dismiss each suggestion
- Confirmed recurring transactions appear in the Monthly Commitments widget
- Auto-entry is created when the next expected date arrives
- Pre-charge alert is sent before the expected date
- Analytics page separates recurring from variable spending
- Detection runs as a background job and does not affect app performance
- No regressions to existing transaction tracking features
- Documentation and UI labels are updated

## 3. Offline Voice Queue - Record Now, Process When Online

Category: Reliability | Difficulty: Intermediate | Repo: voiceyBill-web + voiceyBill-App

### Problem Statement

Voice input currently requires an active internet connection. If there is no connection, the voice feature fails and users lose the moment they intended to record an expense. People on the metro, while traveling, or in low-signal areas need to log expenses immediately and should not have to remember them later.

### Proposed Solution

Introduce an Offline Voice Queue. When a user records a voice entry without internet connectivity, the audio is saved locally in a queue instead of showing an error. When the device comes back online, the queue is processed automatically, the transaction is created, and the user is notified.

### How It Works

1. User records voice while offline - Save audio locally and show a queued message.
2. Audio sits in the local queue - Track id, audioData, recordedAt, status, and error.
3. Device comes back online - Trigger queue processing automatically, send each pending entry through the existing voice pipeline, create the transaction, and mark the entry as processed.
4. User is notified - Show a toast with the number of processed entries. Failed entries remain queued and retry on the next reconnection.

### What This Does Not Include

- No local AI model or WebAssembly
- No on-device transcription
- No changes to the existing online voice pipeline
- No text entry fallback

### Acceptance Criteria

- App correctly detects when the device is offline before attempting voice processing
- Voice recording works normally when offline with no error shown
- Recorded audio is saved to local queue with status pending
- Pending entries are visible to the user in a dedicated UI section
- User can delete a pending entry before it is processed
- Queue triggers automatically when the device comes back online
- Queue processes entries in the order they were recorded
- Each pending entry is sent through the existing AI voice pipeline unchanged
- Successfully processed entries are converted to transactions correctly
- User receives a notification after queue processing completes
- Failed entries remain in the queue with an error message
- Failed entries are retried on the next reconnection
- Queue persists across app restarts
- No changes or regressions to the existing online voice flow
- Works on both web client and React Native app
- Documentation updated

## 4. Multi-Currency Support

Category: Internationalisation | Difficulty: Intermediate | Repo: voiceyBill-server + voiceyBill-web

### Problem Statement

VoiceyBill only supports a single currency per account. Users who travel internationally, work with foreign clients, or manage finances across multiple countries cannot log expenses in different currencies. There is currently no way to log an expense in a foreign currency, see the converted equivalent, or track exchange rates at the time of the transaction.

### Proposed Solution

Introduce Multi-Currency Support across transaction flow, voice input, dashboard, and reports. Users set a base currency in their profile and can log any transaction in any currency. The app stores both the original amount and the converted base currency equivalent.

### Core Functionality

1. Base Currency Setting - Users select a base currency in profile settings.
2. Per-Transaction Currency Selection - Users can enter the transaction in a chosen currency and store the converted amount.
3. Voice Currency Detection - Parse natural speech such as coffee 3 dollars, hotel 80 euros, or taxi 10 pounds.
4. Exchange Rate Fetching - Fetch live exchange rates at creation time and store the rate permanently. Use a cached rate offline with a visible indicator.
5. Unified Dashboard View - Show all totals in the base currency while preserving original and converted amounts per transaction.

### Acceptance Criteria

- User can set a base currency in profile settings
- All supported world currencies are available to select
- User can select a different currency when adding a manual transaction
- Voice input correctly detects currency from natural speech
- If no currency is mentioned in voice input the base currency is used as default
- Live exchange rate is fetched at the time of transaction creation
- Exchange rate is stored permanently with the transaction record
- If offline the last cached exchange rate is used with a visible warning
- Dashboard totals are always displayed in the user's base currency
- Individual transactions show both original and converted amounts
- Category breakdown charts use converted base currency values
- Scheduled email reports display amounts in base currency
- No regressions to existing transaction, voice, or analytics features
- Documentation and UI labels are updated

## 5. Multi-Language UI Support with Urdu

Category: Internationalisation | Difficulty: Intermediate | Repo: voiceyBill-web + voiceyBill-App

### Problem Statement

VoiceyBill's UI is currently only available in English. Voice input already understands Urdu and other languages, but the interface remains English-only. That creates a confusing experience for users who are more comfortable in Urdu or other local languages.

### Proposed Solution

Introduce a full internationalisation system across the web client and React Native app. Users can select a preferred language from Settings. The initial release ships with English as the default and Urdu as the second language. The architecture should allow new languages to be added by introducing translation files without code changes.

### Core Functionality

1. Language Selection in Settings - Add English and Urdu as initial options and allow more languages later.
2. i18n Architecture - Use i18next with react-i18next on both web and React Native, and move all hardcoded UI strings into translation files.
3. RTL Layout Support - Mirror the layout correctly when Urdu is selected, including text alignment, navigation, sidebars, and directional icons.
4. Full UI Coverage - Translate every visible text element including labels, buttons, forms, errors, toasts, empty states, dashboard titles, analytics labels, and settings text.
5. Email Report Localisation - Generate scheduled email reports in the selected language.
6. Contributor Translation Guide - Document how contributors can add a new language by copying the English file, translating values, and opening a pull request.
7. Fallback Behaviour - Fall back to English when a translation key is missing.

### Acceptance Criteria

- User can select a preferred language in Settings
- Selected language is saved to user profile and persists across sessions and devices
- All UI text in the web client is covered by the i18n system with no hardcoded strings
- All UI text in the React Native app is covered by the i18n system with no hardcoded strings
- English translation file is complete and used as the default
- Urdu translation file is complete and correct for the initial release
- Switching language updates the entire UI immediately without a page reload
- RTL layout is applied correctly across the entire app when Urdu is selected
- RTL layout works correctly on both web client and React Native app
- Error messages and toast notifications are translated
- Email reports are generated in the user's selected language
- Fallback to English works correctly when a translation key is missing
- Translation files are structured so a new language can be added without code changes
- A contributor guide for adding new languages is written and included in the repo
- No regressions to existing UI, voice, or transaction features
- Documentation updated

## 6. Conversational Expense Q&A

Category: AI Feature | Difficulty: Intermediate | Repo: voiceyBill-server + voiceyBill-web

### Problem Statement

The Analytics page shows charts for category breakdown, monthly trends, and income versus expense, but those charts only answer predefined questions. Users cannot ask specific questions about their own data and must mentally combine charts or export data manually.

### Proposed Solution

Add an Ask VoiceyBill conversational panel to the Analytics page. Users type or speak natural language questions about their spending. The system uses the AI model already integrated in the project to convert the question into a database query, runs it against the user's own data only, and returns a plain English answer with a supporting mini chart where relevant.

### Core Functionality

1. Natural Language to Query Engine - Send the question and transaction schema description to the AI model, validate the returned pipeline, and run it only against the authenticated user's data.
2. Safety and Security Layer - Allow only a strict whitelist of database operators and reject any query that tries to access another user's data or another collection.
3. Human-Readable Answer Generation - Return plain English answers like spending summaries, top categories, or overspending explanations.
4. Chat UI Panel - Provide conversation history, inline mini charts, and support for both text and voice input.
5. Saved Questions - Let users pin up to five frequently asked questions as quick-access buttons.

### Acceptance Criteria

- User can type a natural language question and receive a relevant answer
- Server correctly converts the question to a database aggregation pipeline via the AI model
- Safety layer rejects any pipeline using disallowed operators
- Safety layer rejects any pipeline attempting to access another user's data
- Results are always scoped to the authenticated user's transactions only
- AI model produces a readable plain English summary from aggregation results
- Chat panel displays correctly on the Analytics page with session history
- Inline mini charts render correctly for numeric results
- Voice input works inside the chat panel
- Users can pin and save up to five frequently asked questions
- Graceful error message shown when the system cannot answer a question
- No financial data is sent to the AI model - only question text and schema description
- No regressions to existing Analytics features
- Documentation updated

## 7. Voice-Powered Group Expense Splitting

Category: Social Finance | Difficulty: Intermediate | Repo: voiceyBill-server + voiceyBill-web + voiceyBill-App

### Problem Statement

Shared expenses are common, but VoiceyBill has no concept of multiple people in one transaction. Users currently have to track shared bills in another app, which breaks the single source of truth and leaves the voice interface unused for a very natural use case.

### Proposed Solution

Extend the existing voice pipeline, transaction schema, and dashboard to support split transactions. When a user logs a shared expense by voice or manually, VoiceyBill records who owes what, tracks settlement status, and sends reminders for unpaid balances.

### Core Functionality

1. Voice Split Detection - Detect split intent and extract the amount, merchant or description, participant names, and split type.
2. Split Transaction Schema - Store a main transaction plus participant split records and a contact list for frequently used names.
3. Balances Dashboard Widget - Show a balances card with contact net balances and full split history.
4. Settlement Flow - Let users mark a split as fully or partially settled and update balances immediately.
5. Automatic Settlement Reminders - Send reminder emails for unsettled splits using the existing cron and Resend setup.
6. Group Trip and Event View - Group related splits under a named event such as a trip, team lunch, or monthly bill cycle.

### Acceptance Criteria

- Voice input correctly detects split intent and extracts participant names and amounts
- Equal split and custom amount split are both supported
- Split transaction is saved correctly with one main transaction plus individual split records per participant
- Balances widget on dashboard shows correct net amounts per contact
- Green and red colour coding works correctly - owed to you versus you owe
- User can mark a split as fully or partially settled
- Settlement correctly updates the remaining net balance
- Reminder email is sent for unsettled splits after the configured number of days
- Contacts list persists and auto-suggests names from past splits
- Multiple splits can be grouped under a named event or trip
- Split history is viewable per contact
- Net balances are correctly calculated across all unsettled splits
- Voice pipeline changes do not break existing single-user voice entries
- No regressions to existing transaction, analytics, or report features
- Documentation and UI labels are updated
