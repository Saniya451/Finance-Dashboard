# Finance Dashboard UI - Complete Documentation

A modern, interactive Finance Dashboard built with React 18, Vite, and Tailwind CSS. This comprehensive project demonstrates a complete frontend implementation of a financial tracking application with role-based access, data persistence, and rich analytics.

**Status**: ✅ Production Ready | 🎨 Fully Styled | 📱 Mobile Responsive | 🔒 Role-Based Access

---

## 📋 Table of Contents

1. [Quick Start](#quick-start)
2. [Project Architecture & Flow](#project-architecture--flow)
3. [How This Project Was Built](#how-this-project-was-built)
4. [Core Features](#core-features)
5. [Advanced Features](#advanced-features)
6. [Tech Stack](#tech-stack)
7. [Project Structure](#project-structure)
8. [Assignment Requirements Checklist](#assignment-requirements-checklist)
9. [Data Models](#data-models)
10. [State Management](#state-management)
11. [Usage Guide](#usage-guide)
12. [Customization](#customization)
13. [Browser Support](#browser-support)

---

## 🚀 Quick Start

### Prerequisites
- Node.js v14+
- npm or yarn

### Installation & Running

```bash
# Install dependencies
npm install

# Start development server (runs on http://localhost:5174)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

---

## 🏗️ Project Architecture & Flow

### High-Level Application Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                         App Component                           │
│                    (Main State Container)                       │
│                                                                 │
│  - Manages transactions, filters, role, theme, sidebar state   │
│  - Persists data to localStorage                               │
│  - Handles responsive sidebar behavior                         │
└────────────────────┬────────────────────────────────────────────┘
                     │
        ┌────────────┴────────────┬──────────────┬──────────────┐
        │                         │              │              │
        ▼                         ▼              ▼              ▼
   ┌─────────┐          ┌──────────────┐  ┌─────────┐  ┌───────────┐
   │ Header  │          │   Sidebar    │  │ DashOvr │  │ Trans Sec │
   │         │          │              │  │         │  │           │
   │ - Menu  │          │ Dashboard    │  │ Summary │  │ Filters   │
   │ - Theme │          │ Transactions │  │ Charts  │  │ Table     │
   │ - Role  │          │ Insights     │  │         │  │ Form      │
   │ - Export│          │ Settings     │  │         │  │           │
   └─────────┘          └──────────────┘  └─────────┘  └───────────┘
        │                                                     │
        │                                    ┌────────────────┘
        │                                    │
        └────────────────────────┬───────────┘
                                 │
                    ┌────────────┴────────────┐
                    │                         │
                    ▼                         ▼
            ┌──────────────────┐    ┌─────────────────┐
            │   localStorage   │    │ Mock Data Gen   │
            │                  │    │                 │
            │ - transactions   │    │ Income/Expense  │
            │ - dark_mode      │    │ Categories      │
            └──────────────────┘    └─────────────────┘
```

### Data Flow Architecture

```
User Input
    │
    ├─→ Header (Role/Theme)
    ├─→ Sidebar (Navigation)
    ├─→ TransactionForm (Add/Edit)
    ├─→ TransactionFilters (Filter)
    │
    ▼
App State Update
    │
    ├─→ setTransactions()
    ├─→ setRole()
    ├─→ setFilters()
    ├─→ setSidebarOpen()
    │
    ▼
useEffect Hook
    │
    ├─→ Save to localStorage
    ├─→ Calculate derived state
    │
    ▼
Component Re-render
    │
    ├─→ DashboardOverview (Analytics)
    ├─→ TransactionTable (Display)
    ├─→ Charts (Visualizations)
    ├─→ Insights (Calculations)
    │
    ▼
User Sees Updated UI
```

### Component Interaction Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         App.jsx                                 │
│  State: transactions, filters, role, isDark, sidebarOpen        │
│  Handlers: Add, Edit, Delete, Filter, Sort, Reset              │
└────────────┬────────────────────────────────────────────────────┘
             │
             ├─────────────────────────────────┬──────────────────┐
             │                                 │                  │
        ┌────▼────┐                    ┌──────▼──────┐    ┌──────▼──────┐
        │ Header  │                    │  Sidebar   │    │MainContent  │
        ├─────────┤                    ├────────────┤    ├─────────────┤
        │ isDark  │◄────────────────►  │ activeSec  │    │ activeSection
        │ role    │   toggle, switch   │ sidebarOpen │   │             │
        │ onRoleChg       menu        └────────────┘   │ Navigator   │
        └─────────┘                                     │             │
                                                        └────┬────────┘
                                                             │
                            ┌────────────────┬──────────────┼──────────────┐
                            │                │              │              │
                       ┌────▼────┐    ┌─────▼────┐   ┌────▼──────┐  ┌───▼────────┐
                       │Dashboard│    │Transact  │   │ Insights  │  │ Settings  │
                       │Overview │    │ Section  │   │Section    │  │           │
                       ├─────────┤    ├──────────┤   ├───────────┤  ├───────────┤
                       │Summary  │    │ Filters  │   │ Analytics │  │Role Info  │
                       │Cards    │    │ Table    │   │ Insights  │  │Data Mgmt  │
                       │Charts   │    │ Form     │   │ Stats     │  │Reset Btn  │
                       └─────────┘    └──────────┘   └───────────┘  └───────────┘
```

---

## 🛠️ How This Project Was Built

### Phase 1: Project Setup (Foundation)
1. **Created Vite React project** with template
2. **Installed dependencies**:
   - React 18 (UI library)
   - Tailwind CSS (styling)
   - Recharts (charting)
   - Lucide React (icons)
3. **Configured build tools**:
   - vite.config.js (bundling)
   - tailwind.config.js (styling config)
   - postcss.config.js (CSS processing)

### Phase 2: Component Architecture (Structure)
1. **Created component hierarchy**:
   - Header component (top navigation)
   - Sidebar component (navigation menu)
   - Summary cards (statistics displays)
   - Charts (Recharts integration)
   - Transaction table (data display)
   - Forms (data input)

2. **Created custom hooks**:
   - `useDarkMode` - dark mode state management
   - `useFilteredTransactions` - transaction filtering logic

3. **Created utilities**:
   - `mockData.js` - generates realistic dummy data
   - `analytics.js` - calculations & insights logic

### Phase 3: State Management (Logic)
1. **Implemented React hooks**:
   - useState for local component state
   - useEffect for side effects (localStorage, responsive behavior)
   - useMemo for optimization (filtered transactions)

2. **Created data flow patterns**:
   - Props drilling for simple state passing
   - Callback functions for child→parent communication
   - useEffect for data persistence

3. **Added localStorage integration**:
   - Auto-save transactions on every change
   - Auto-load transactions on app startup
   - Persist dark mode preference

### Phase 4: Styling & Theming (Design)
1. **Configured Tailwind CSS**:
   - Custom color palette (blue primary)
   - Dark mode support (class-based)
   - Custom animations (fade-in, slide-in)
   - Responsive breakpoints (mobile-first)

2. **Implemented dark mode**:
   - Toggle button in header
   - Auto-applied with dark: prefix
   - Persisted preference

3. **Responsive design**:
   - Mobile hamburger menu
   - Sidebar collapse/expand
   - Adaptive layouts

### Phase 5: Features Implementation (Functionality)
1. **Dashboard Overview**:
   - Summary cards showing balance, income, expenses
   - Balance trend chart (last 10 days)
   - Spending breakdown pie chart

2. **Transactions Management**:
   - Display all transactions in table
   - Add new transactions (admin only)
   - Edit existing transactions (admin only)
   - Delete transactions (admin only)
   - Filter by type/category/date/search
   - Sort by date/amount/category
   - Export as CSV/JSON

3. **Role-Based Access**:
   - Viewer role (read-only)
   - Admin role (full CRUD)
   - Role switcher in header
   - Conditional rendering of admin features

4. **Insights Section**:
   - Calculate highest spending category
   - Calculate savings rate
   - Monthly spending comparison
   - Average daily spending
   - Income vs expense analysis
   - Most frequent spending category

5. **Settings Section**:
   - View current role
   - Reset data functionality
   - Data management info

### Phase 6: Polish & Optimization (Refinement)
1. **Performance optimization**:
   - useMemo for expensive calculations
   - Lazy loading where applicable
   - CSS animations for UI smoothness

2. **Bug fixes**:
   - Fixed hamburger menu visibility
   - Fixed sidebar responsive behavior
   - Fixed overlay click handling
   - Fixed menu item close on mobile

3. **Enhanced mock data**:
   - 60 days of transactions (vs 30)
   - Multiple expenses per day
   - Consistent income pattern
   - 24 different transaction types
   - Proper timestamps with hours/minutes

### Phase 7: Testing & Validation
1. **Manual testing**:
   - Desktop responsiveness
   - Mobile responsiveness
   - Role-based functionality
   - Dark mode toggle
   - Data persistence
   - Filter/sort operations
   - Add/edit/delete operations

2. **Browser testing**:
   - Chrome
   - Firefox
   - Safari

---

## ✨ Core Features

### 1. Dashboard Overview
- **Summary Cards**:
  - Total Balance (updated in real-time)
  - Month
's Income (calculated from transactions)
  - Month's Expenses (calculated from transactions)
  - Savings Rate (percentage calculation)
  - 📈 Trend indicators showing direction

- **Balance Trend Chart**:
  - Line chart showing last 10 days
  - Interactive tooltips
  - Responsive sizing

- **Spending Breakdown Chart**:
  - Pie chart by category
  - Category-specific colors
  - Interactive legend
  - Expense distribution

### 2. Transactions Management
- **Transaction Table**:
  - Display date, type, category, description, amount
  - Color-coded income (green) / expense (red)
  - Responsive table design
  - Admin edit/delete buttons

- **Advanced Filtering**:
  - Filter by type (All, Income, Expense)
  - Filter by category (dynamically populated)
  - Filter by date range (All, Today, This Week, This Month, This Year)
  - Search by description (real-time)
  - Chainable filters

- **Sorting Options**:
  - By date (newest/oldest)
  - By amount (highest/lowest)
  - By category (A-Z)

- **Add/Edit Transactions** (Admin only):
  - Form with validation
  - Date, type, category, amount, description fields
  - Modal dialog interface
  - Auto-close on save

### 3. Role-Based Access Control
- **Viewer Role**:
  - View all dashboards and reports
  - View transaction history
  - View insights
  - NO add/edit/delete capabilities
  - Read-only filters and exports

- **Admin Role**:
  - Full dashboard access
  - Add new transactions
  - Edit existing transactions
  - Delete transactions
  - Reset data
  - All viewer capabilities

- **Role Switcher**:
  - Dropdown in header
  - Real-time role switching
  - Visual indicators in settings

### 4. Insights & Analytics
- **Smart Calculations**:
  - Highest spending category
  - Savings rate (income - expenses / income)
  - Monthly spending trend
  - Average daily spending
  - Income vs expense breakdown
  - Most frequent spending category

- **Insight Cards**:
  - Visual presentation of insights
  - Icons for each insight type
  - Color-coded indicators

### 5. Settings & Configuration
- **Role Management**:
  - View current role
  - Understanding role differences
  - Admin-only features clearly marked

- **Data Management**:
  - Reset to mock data button
  - Confirmation before reset
  - Admin-only operation

---

## ⚙️ Advanced Features

### 1. Dark Mode
- **Toggle Button**: Sun/Moon icon in header
- **Persistent**: Preference saved in localStorage
- **Smooth Transitions**: CSS transitions for theme switching
- **Consistent Styling**: Applied throughout entire app

### 2. Data Persistence
- **Automatic Saving**: Changes saved to localStorage instantly
- **Automatic Loading**: Data restored on app startup
- **localStorage Keys**:
  - `dashboard_transactions`: Transaction array
  - `dashboard_dark_mode`: Boolean preference

### 3. Export Functionality
- **CSV Export**:
  - Downloads as spreadsheet-compatible format
  - All transaction data included
  - Date-stamped filename

- **JSON Export**:
  - Downloads as JSON file
  - Raw data format
  - Date-stamped filename

- **Export Button**: Located in Transactions section (visible to all roles)

### 4. Responsive Design
- **Mobile (< 768px)**:
  - Hamburger menu visible
  - Sidebar collapses/expands
  - Single column layouts
  - Touch-friendly buttons

- **Tablet (768px - 1024px)**:
  - Sidebar visible
  - Adjustable layouts
  - Optimized spacing

- **Desktop (> 1024px)**:
  - Full sidebar always visible
  - Multi-column layouts
  - Optimal content distribution

### 5. Animations & Transitions
- **Fade-in animations**: Components appear smoothly
- **Slide-in animations**: Sidebar slide animation
- **Hover effects**: Button and link states
- **Smooth theme transitions**: Dark mode changes smoothly

### 6. Form Validation
- **Required fields**: Enforced on submission
- **Amount validation**: Only accepts valid numbers
- **Category validation**: Selection from predefined list
- **Type validation**: Income/Expense selection

---

## 🏛️ Tech Stack

| Category | Technology | Version | Purpose |
|----------|-----------|---------|---------|
| **Framework** | React | 18 | UI library |
| **Build Tool** | Vite | 4.4 | Fast bundling |
| **Styling** | Tailwind CSS | 3.3 | Utility CSS |
| **CSS Processing** | PostCSS | Latest | CSS transformation |
| **Charts** | Recharts | 2.10 | Data visualization |
| **Icons** | Lucide React | 0.263 | SVG icons |
| **State** | React Hooks | Built-in | State management |
| **Storage** | LocalStorage | Built-in | Data persistence |

---

## 📁 Project Structure

```
assignment ui project/
├── src/
│   ├── components/
│   │   ├── Header.jsx                 # Navigation bar with theme/role toggle
│   │   ├── Sidebar.jsx                # Collapsible navigation sidebar
│   │   ├── SummaryCard.jsx            # Reusable summary statistic card
│   │   ├── BalanceTrendChart.jsx      # Line chart showing balance trend
│   │   ├── SpendingBreakdownChart.jsx # Pie chart of spending by category
│   │   ├── TransactionTable.jsx       # Table displaying transactions
│   │   ├── TransactionFilters.jsx     # Filter controls for transactions
│   │   ├── TransactionForm.jsx        # Form for adding/editing transactions
│   │   └── InsightCard.jsx            # Display individual financial insights
│   │
│   ├── sections/
│   │   ├── DashboardOverview.jsx      # Main dashboard page
│   │   ├── TransactionsSection.jsx    # Transactions management page
│   │   └── InsightsSection.jsx        # Financial insights page
│   │
│   ├── hooks/
│   │   ├── useDarkMode.js             # Dark mode state hook
│   │   └── useFilteredTransactions.js # Transaction filtering hook
│   │
│   ├── utils/
│   │   ├── mockData.js                # Mock transaction generator
│   │   └── analytics.js               # Calculation & filtering utilities
│   │
│   ├── App.jsx                        # Root component (main state container)
│   ├── main.jsx                       # React DOM entry point
│   └── index.css                      # Global styles
│
├── public/
│   └── vite.svg                       # Vite logo
│
├── index.html                         # HTML entry point
├── package.json                       # Dependencies & scripts
├── tailwind.config.js                 # Tailwind configuration
├── postcss.config.js                  # PostCSS configuration
├── vite.config.js                     # Vite configuration
└── README.md                          # This file
```

---

## ✅ Assignment Requirements Checklist

### 1. Dashboard Overview ✅
- [x] Summary cards (Balance, Income, Expenses, Savings Rate)
- [x] Time-based visualization (Balance Trend - Line Chart)
- [x] Categorical visualization (Spending Breakdown - Pie Chart)
- [x] Real-time data updates

### 2. Transactions Section ✅
- [x] Display transaction list (date, amount, category, type)
- [x] Basic filtering (type, category, date range, search)
- [x] Sorting (by date, amount, category)
- [x] Admin add transactions
- [x] Admin edit transactions
- [x] Admin delete transactions

### 3. Basic Role-Based UI ✅
- [x] Viewer role (read-only)
- [x] Admin role (full CRUD)
- [x] Role switcher dropdown
- [x] Conditional rendering based on role
- [x] Clear admin-only labels

### 4. Insights Section ✅
- [x] Highest spending category
- [x] Monthly spending comparison
- [x] Savings rate calculation
- [x] Average daily spending
- [x] Income vs expense analysis
- [x] Most frequent spending category

### 5. State Management ✅
- [x] Handle transactions data
- [x] Handle filters state
- [x] Handle role selection
- [x] Proper React Hooks usage
- [x] useEffect for side effects
- [x] useMemo for optimization

### 6. UI & UX ✅
- [x] Clean, readable design
- [x] Mobile responsive (< 768px)
- [x] Tablet responsive (768px - 1024px)
- [x] Desktop responsive (> 1024px)
- [x] Empty data handling
- [x] Smooth animations
- [x] Intuitive navigation

### 7. Optional Enhancements ✅
- [x] **Dark Mode** - Toggle with persistent storage
- [x] **Data Persistence** - localStorage integration
- [x] **Animations** - Fade-in, slide-in transitions
- [x] **Export Functionality** - CSV and JSON export
- [x] **Enhanced Filtering** - Multiple filter types
- [x] **Responsive Design** - Mobile hamburger menu
- [x] **Mock Data** - 60 days of realistic transactions

### 8. Documentation ✅
- [x] Clear README with setup instructions
- [x] Architecture overview
- [x] Component descriptions
- [x] Usage guide
- [x] Tech stack documentation
- [x] How it was built documentation

---

## 📊 Data Models

### Transaction Object
```javascript
{
  id: number,                      // Unique identifier
  date: string (ISO format),       // Transaction date & time
  type: 'income' | 'expense',      // Transaction type
  category: string,                // Category (Food, Transport, etc.)
  description: string,             // Transaction description
  amount: number                   // Amount (negative for expenses)
}
```

### Filter Object
```javascript
{
  type: 'all' | 'income' | 'expense',     // Filter by type
  category: 'all' | string,               // Filter by category
  searchTerm: string,                     // Search in description
  dateRange: 'all' | 'today' | 'week' | 'month' | 'year'  // Date filter
}
```

### App State
```javascript
{
  transactions: Transaction[],         // All transactions
  filters: Filter,                     // Active filters
  sortBy: string,                      // Sort field
  role: 'viewer' | 'admin',           // User role
  isDark: boolean,                     // Dark mode status
  sidebarOpen: boolean,                // Sidebar visibility
  activeSection: string                // Current page
}
```

---

## 🔄 State Management

### Key State Variables (in App.jsx)
- **transactions**: Array of all transaction objects
- **filters**: Current filter settings
- **sortBy**: Current sort field
- **role**: User role (viewer/admin)
- **isDark**: Dark mode enabled/disabled
- **sidebarOpen**: Sidebar open/closed state
- **activeSection**: Currently active section/page

### State Update Patterns
1. **Add Transaction**: `setTransactions([newTx, ...transactions])`
2. **Edit Transaction**: `setTransactions(map and replace)`
3. **Delete Transaction**: `setTransactions(filter out)`
4. **Filter Changes**: `setFilters({...})`
5. **Role Change**: `setRole(newRole)`
6. **Toggle Theme**: `toggleDarkMode()`
7. **Toggle Sidebar**: `setSidebarOpen(!open)`

### useEffect Hooks
1. **Initialize mock data**: Runs once on mount
2. **Load localStorage**: Runs once on mount
3. **Save to localStorage**: Runs whenever transactions change
4. **Responsive sidebar**: Handles window resize events

---

## 📖 Usage Guide

### First Time Setup
1. Open the dashboard
2. See it pre-populated with 60 days of mock data
3. Dashboard shows summary cards and charts

### Viewing Data
- **Dashboard**: See summary cards, charts, balance trend
- **Transactions**: Browse all transactions with filters/sorting
- **Insights**: View financial analytics
- **Settings**: See role info and data management

### Filtering Transactions
1. Go to Transactions section
2. Use filter dropdowns:
   - **Type**: Income, Expense, All
   - **Category**: Select specific category
   - **Date Range**: Today, Week, Month, Year, All
   - **Search**: Type in search box
3. Filters chain together (AND logic)

### Sorting Transactions
1. Go to Transactions section
2. Use Sort dropdown:
   - By Date (newest first)
   - By Amount (highest first)
   - By Category (A-Z)

### Adding Transactions (Admin)
1. Change role to Admin
2. Click "Add Transaction" button
3. Fill in form:
   - Date
   - Type (Income/Expense)
   - Category
   - Amount
   - Description
4. Click Submit

### Editing Transactions (Admin)
1. Find transaction in table
2. Click edit icon (pencil)
3. Modify values in form
4. Click Submit

### Deleting Transactions (Admin)
1. Find transaction in table
2. Click delete icon (trash)
3. Confirm deletion

### Exporting Data
1. Go to Transactions section
2. Click Export button
3. Choose format:
   - CSV (for Excel/spreadsheet)
   - JSON (for data backup)
4. File downloads automatically

### Toggling Dark Mode
1. Click Moon/Sun icon in header
2. Theme switches immediately
3. Preference is saved

### Switching Roles
1. Use dropdown in header
2. Select Viewer or Admin
3. UI updates accordingly
4. Admin features appear/disappear

### Resetting Data
1. Go to Settings section
2. Change to Admin role if needed
3. Click "Reset to Mock Data"
4. Confirm reset
5. Dashboard reloads with original mock data

---

## 🎨 Customization

### Adding New Transaction Categories
1. Edit `CATEGORIES` in `src/components/TransactionForm.jsx`
2. Update mock data in `src/utils/mockData.js`
3. Add colors in `SpendingBreakdownChart.jsx` if needed

### Changing Color Scheme
Edit `tailwind.config.js`:
```javascript
extend: {
  colors: {
    // Change primary color
    blue: '...'
  }
}
```

### Adjusting Responsive Breakpoints
Edit `tailwind.config.js` or override in component:
```javascript
// Current breakpoint: md (768px)
className="hidden md:block"  // Hidden on mobile, shown on 768px+
```

### Modifying Chart Data Range
Edit functions in `src/utils/analytics.js`:
- `getBalanceTrendData()` - Change 10 days to different range
- `getCategoryBreakdown()` - Filter different expenses

### Styling Customization
- Global styles: `src/index.css`
- Tailwind config: `tailwind.config.js`
- Individual components: Modify className attributes

---

## 🌐 Browser Support

### Supported Browsers
- ✅ Chrome/Chromium (latest)
- ✅ Firefox (latest)
- ✅ Safari (latest)
- ✅ Edge (latest)

### Required Features
- ES2020+ JavaScript support
- CSS Grid & Flexbox
- localStorage API
- SVG support

---

## 📈 Performance Notes

- **useMemo**: Used on filtered transactions to prevent recalculation
- **Lazy Loading**: Form modal loads on demand
- **Hardware Acceleration**: CSS animations use `transform` and `opacity`
- **Efficient Rendering**: Components only re-render when state changes
- **localStorage Index**: ~50KB of typical data

---

## 🎯 Key Accomplishments

1. ✅ **Complete Feature Set**: All requirements met + enhancements
2. ✅ **Clean Architecture**: Well-organized components and hooks
3. ✅ **Professional Design**: Modern UI with smooth animations
4. ✅ **Fully Responsive**: Works on all device sizes
5. ✅ **Data Persistence**: Automatic localStorage integration
6. ✅ **Role-Based Access**: Proper RBAC simulation
7. ✅ **Rich Analytics**: Multiple insight calculations
8. ✅ **User Experience**: Intuitive navigation and interactions
9. ✅ **Code Quality**: Modular, maintainable, well-commented
10. ✅ **Documentation**: Comprehensive README and inline comments

---

## 🚀 Future Enhancement Ideas

- Backend API integration (Node.js, Python, Firebase)
- User authentication (JWT, OAuth)
- Multiple accounts/wallets
- Recurring transactions
- Budget planning & alerts
- Bill reminders
- Multi-currency support
- Advanced reporting & pdf export
- Mobile app (React Native)
- Transaction tagging/labeling
- Scheduled transactions
- Receipt uploads
- Smart categorization
- Spending goals

---

## 📝 Project Notes

This project demonstrates a complete modern frontend application following React best practices:
- Component composition and reusability
- State management with React Hooks
- Custom hook creation
- localStorage API usage
- Responsive design principles
- Tailwind CSS mastery
- Form handling and validation
- Data filtering and sorting
- Charts and data visualization
- Role-based access control
- Dark mode implementation

All without any backend dependencies - a true frontend-only application!

---

## 📋 Assignment Submission Form

### Primary Framework or Library Used
**React.js with JavaScript**

### Features Implemented
- ✅ Dashboard Overview with Summary Cards
- ✅ Time Based Visualization (e.g., Balance Trend)
- ✅ Categorical Visualization (e.g., Spending Breakdown)
- ✅ Transaction List with Details
- ✅ Transaction Filtering
- ✅ Transaction Sorting or Search
- ✅ Role Based UI (Viewer and Admin)
- ✅ Insights Section
- ✅ State Management (Context, Redux, Zustand, etc.)
- ✅ Responsive Design

### Technical Decisions and Trade-offs

**Framework Choice: React.js with JavaScript**
- Selected React.js for its component-based architecture and excellent ecosystem
- Chose JavaScript over TypeScript for simplicity and faster development iteration
- Trade-off: TypeScript would provide better type safety but increases complexity for a frontend-only assignment

**Styling Approach: Tailwind CSS**
- Used Tailwind CSS for rapid UI development and consistent design system
- Implemented utility-first approach for maintainable and responsive styling
- Trade-off: Larger CSS bundle size vs. faster development and consistent design

**State Management Strategy: React Hooks (useState, useEffect, useMemo)**
- Leveraged built-in React hooks for local state management
- Used useState for component state, useEffect for side effects, useMemo for performance optimization
- Chose simple React hooks over external libraries (Redux, Zustand) to keep the codebase lightweight
- Trade-off: Manual state lifting vs. simpler architecture without external dependencies

**Data Persistence: Browser localStorage**
- Implemented client-side persistence using localStorage API
- Automatic save/load of transactions and user preferences
- Trade-off: No backend required vs. data loss if localStorage is cleared

**Build Tool: Vite**
- Fast development server with hot module replacement
- Optimized production builds with tree-shaking
- Trade-off: Modern tooling vs. broader compatibility with older build systems

**Charting Library: Recharts**
- React-native charting library for data visualizations
- Interactive and responsive charts out-of-the-box
- Trade-off: Additional dependency vs. pre-built chart components

**Icon Library: Lucide React**
- Modern SVG icons with consistent design
- Tree-shakable for optimal bundle size
- Trade-off: External dependency vs. custom SVG icons

### Additional Notes

**Project Scope and Limitations:**
- Built as a frontend-only application without backend dependencies
- All data is mock-generated and persisted in browser localStorage
- No user authentication or multi-user support (simulated with role-based UI)
- Charts show data for the last 10 days (configurable in analytics.js)

**Key Strengths:**
- Complete feature implementation meeting all assignment requirements
- Professional UI/UX with dark mode, animations, and responsive design
- Clean, maintainable code structure with proper separation of concerns
- Comprehensive documentation and setup instructions
- Enhanced with optional features (export, animations, advanced filtering)

**Areas for Potential Improvement:**
- Could integrate with a real backend API for data persistence
- TypeScript integration for better type safety
- Unit tests for component and utility functions
- Progressive Web App (PWA) features for offline functionality
- Advanced analytics with more sophisticated calculations

**Development Approach:**
- Mobile-first responsive design with Tailwind CSS breakpoints
- Component composition for reusability and maintainability
- Custom hooks for shared logic (useDarkMode, useFilteredTransactions)
- Performance optimization with useMemo for expensive calculations
- Accessibility considerations with proper ARIA labels and keyboard navigation

**Browser Compatibility:**
- Tested on Chrome, Firefox, Safari, and Edge
- ES2020+ JavaScript features used (modern browser support assumed)
- CSS Grid and Flexbox for layout (supported in all modern browsers)

---

**Built with** ❤️ **using React, Vite, and Tailwind CSS**

├── hooks/
│   ├── useDarkMode.js          # Dark mode toggle hook
│   └── useFilteredTransactions.js # Transaction filtering hook
├── utils/
│   ├── mockData.js             # Mock transaction data
│   └── analytics.js            # Data calculation and filtering utilities
├── App.jsx                     # Main app component
├── main.jsx                    # React DOM entry point
└── index.css                   # Global styles
```

## Getting Started

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Install dependencies:
```bash
npm install
```

2. Start the development server:
```bash
npm run dev
```

3. Open your browser and navigate to `http://localhost:5173`

### Building for Production

```bash
npm run build
```

The built files will be in the `dist/` directory.

## Usage

### Dashboard Overview
- View summary cards showing your financial snapshot
- See balance trends over the last 10 days
- Check spending breakdown by category
- View quick statistics

### Transactions
- **Filtering**: Filter by type (income/expense), category, date range, and search by description
- **Sorting**: Sort by date, amount, or category
- **Admin Actions**: 
  - Click "Add Transaction" to create a new transaction
  - Click the edit icon to modify an existing transaction
  - Click the delete icon to remove a transaction
- **Export**: Export all transactions as CSV or JSON

### Role-Based Access

#### Viewer Role
- View all data and reports
- Cannot add, edit, or delete transactions
- Read-only access to the dashboard

#### Admin Role
- Full access to all features
- Add new transactions
- Edit existing transactions
- Delete transactions
- Reset data to mock data

Switch roles using the role dropdown in the header.

### Insights
- View your highest spending category
- Check your savings rate
- See monthly spending comparison
- View average daily spending
- Track income vs expenses
- Identify most frequent spending categories

### Settings
- Switch between roles
- Reset data to original mock data
- View data persistence information

## State Management

The app uses React's `useState` and `useEffect` hooks for state management:
- **Transactions**: Array of transaction objects
- **Filters**: Object containing current filter values
- **Theme**: Boolean for dark mode
- **Role**: Current user role (viewer/admin)
- **Sidebar**: Mobile sidebar toggle state

### Data Persistence
- Transactions are persisted to `localStorage` with key `dashboard_transactions`
- Dark mode preference is persisted with key `dashboard_dark_mode`
- Data is automatically saved on every change

## Mock Data

The app comes pre-loaded with mock transaction data for the last 30 days, including:
- Income transactions (salary, freelance, bonus)
- Expense transactions across multiple categories (food, transport, entertainment, utilities, healthcare, shopping)

Data is generated fresh on app load unless there's existing data in localStorage.

## Responsive Design

The dashboard is fully responsive:
- **Mobile (< 768px)**: Sidebar hidden by default, collapsible navigation
- **Tablet (768px - 1024px)**: Sidebar visible on smaller screens
- **Desktop (> 1024px)**: Full layout with visible sidebar

## Customization

### Adding New Categories
Edit the `CATEGORIES` array in `src/components/TransactionForm.jsx` and `src/utils/mockData.js`

### Changing Colors
Modify the Tailwind color scheme in `tailwind.config.js`

### Adjusting Chart Data Range
Edit the data calculation functions in `src/utils/analytics.js`

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Performance Considerations

- Uses `useMemo` for filtered transactions to prevent unnecessary recalculations
- LocalStorage is used for fast, client-side persistence
- Charts are optimized with Recharts for smooth rendering
- CSS animations use hardware acceleration

## Future Enhancements

- Backend API integration
- User authentication
- Multiple accounts/wallets
- Recurring transactions
- Budget planning
- Bill reminders
- Multi-currency support
- Advanced reporting

## License

This project is open source and available under the MIT License.

## Author

Created as a Finance Dashboard UI assignment project.
