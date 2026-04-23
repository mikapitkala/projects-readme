# 🏁 Beachside Racetrack Management System

A comprehensive real-time race management system for managing racing sessions, lap timing, and leaderboards. This **MVP (Minimum Viable Product)** provides all essential features needed to run a professional race track operation.

> **What is MVP?** A Minimum Viable Product contains the core features needed to solve the main problem - in this case, managing races from start to finish with real-time updates and multiple user interfaces.

## 📋 Table of Contents

- 🚀 **[Install the system](#-installation)** - Get up and running in 5 minutes
- 🏁 **[Start my first race](#-usage-examples)** - Complete workflow guide
- 🎯 **[See all features](#-features-overview)** - What the system can do
- 🔐 **[Configure access keys](#-authentication--configuration)** - Security setup
- 🛠️ **[Set up development](#-development-guide)** - Development and testing
- 🏗️ **[Understand architecture](#-technical-architecture)** - Technical details
- 🔧 **[Customize settings](#-customization)** - Race timing and configuration

**📚 Complete Documentation:**

- **[INSTALLATION.md](docs/INSTALLATION.md)** - Detailed setup guide for beginners
- **[ARCHITECTURE.md](docs/ARCHITECTURE.md)** - Technical architecture and relationships
- **[NGROK_SETUP.md](docs/NGROK_SETUP.md)** - Remote access setup for testing
- **[.env example](.env%20example)** - Environment configuration template

---

## 🚀 Installation

### Prerequisites

- **Node.js** (v16 or higher) - [Download here](https://nodejs.org)
- **npm** (comes with Node.js)
- **Git** (optional, for cloning)

### Quick Setup (5 minutes)

1. **Install dependencies:**

   ```bash
   git clone <repository-url>
   cd race-track
   npm install
   ```

2. **Create environment file:**

   ```bash
   cp ".env example" .env
   ```

3. **Start with sample data:**

   ```bash
   npm run "dev testData"
   ```

4. **Open in browser:**

   ```text
   http://localhost:3000/dashboard
   ```

### Run Options

Choose the right mode for your needs:

**🎯 First Time / Demo** (Recommended):
```bash
npm run "dev testData"
```
⚠️ **WARNING**: This command will **DELETE ALL EXISTING DATA**!
- **RESETS** all racing sessions and lap times
- **ASKS FOR CONFIRMATION** before proceeding
- Creates 3 fresh sample racing sessions
- Short 60-second races for testing
- Perfect for exploration and first-time setup

**🛠️ Development Mode**:
```bash
npm run dev
```
- Short races + detailed logging
- Keeps existing data
- File logging to `data/log.log`

**🏁 Production Mode**:
```bash
npm start
```
- Full 10-minute races
- Silent operation
- Optimized performance

### Default Access Keys

- **Front Desk (Receptionist)**: `111`
- **Race Control (Safety Officer)**: `222`
- **Lap Line Tracker (Observer)**: `333`

📋 **Need detailed instructions?** See [INSTALLATION.md](docs/INSTALLATION.md)

---

<a id="usage-examples"></a>
## 🏁 Usage Examples

### Complete Race Workflow

**1. Create a Racing Session** (Front Desk)
- Go to `http://localhost:3000/front-desk` → Login with `111`
- Click "Create Session" → Add session name
- Add drivers: "John Doe", "Jane Smith", "Mike Johnson"
- Assign cars automatically or manually
- Lock session when ready

**2. Start the Race** (Race Control)
- Go to `http://localhost:3000/race-control` → Login with `222`
- Select the locked session
- Click "Start Race" → Green flag appears
- Monitor race progress and safety

**3. Record Lap Times** (Lap Tracker)
- Go to `http://localhost:3000/lap-line-tracker` → Login with `333`
- Select drivers as they cross finish line
- Times are recorded automatically
- Leaderboard updates in real-time

**4. View Live Results** (Public Display)
- Open `http://localhost:3000/leader-board` (no login needed)
- Watch live race standings
- See fastest lap times
- Display on big screens for spectators

**5. Monitor Everything** (Dashboard)
- Go to `http://localhost:3000/dashboard` (no login needed)
- View all interfaces in one window
- Minimize/maximize windows as needed
- Perfect for race control center

### Quick Test Scenario

After running `npm run "dev testData"`:

1. **Dashboard**: Open `http://localhost:3000/dashboard`
2. **Start Race**: Click Race Control window → Login `222` → Start any session
3. **Record Laps**: Click Lap Tracker window → Login `333` → Record some laps
4. **Watch Results**: See leaderboard update automatically
5. **Manage Sessions**: Click Front Desk window → Login `111` → Add more drivers

---

<a id="features-overview"></a>
## 🎯 Features Overview

### Core Management Interfaces

| Interface | Access | Purpose | Key Features |
|-----------|--------|---------|--------------|
| **🏎️ Front Desk** | `111` | Session Management | Create sessions, register drivers, assign cars |
| **🏆 Race Control** | `222` | Race Operations | Start/stop races, safety flags, monitoring |
| **⏱️ Lap Tracker** | `333` | Timing | Record lap times, fastest lap tracking |

### Public Display Interfaces

| Interface | Access | Purpose | Key Features |
|-----------|--------|---------|--------------|
| **🏁 Leaderboard** | Public | Live Results | Real-time standings, lap counts, race status |
| **📋 Next Race** | Public | Queue Info | Upcoming drivers, car assignments |
| **🚩 Race Flags** | Public | Status Display | Visual flag indicators, color-coded states |
| **📊 Dashboard** | Public | Control Center | All interfaces, window management |

### Key Capabilities

- **🔄 Real-time Updates**: Instant synchronization across all interfaces
- **👥 Multi-user Support**: Multiple staff can work simultaneously  
- **📱 Mobile Responsive**: Works on desktop, tablet, and mobile
- **🔒 Role-based Security**: Different access levels for different staff
- **💾 Auto Recovery**: System restores state after interruptions
- **⚡ Fast Setup**: Running in 5 minutes with sample data

---

<a id="authentication-configuration"></a>
## 🔐 Authentication & Configuration

### Environment Setup

The system uses simple key-based authentication. Edit your `.env` file:

```bash
# Staff Access Keys
RECEPTIONIST_KEY=your_front_desk_key    # Front Desk access
SAFETY_KEY=your_race_control_key        # Race Control access  
OBSERVER_KEY=your_lap_tracker_key       # Lap Tracker access
```

### Security Features

- **Role Separation**: Each interface requires specific authentication
- **Session Persistence**: Login remembered during browser session
- **Public Displays**: Leaderboard, flags, dashboard require no authentication
- **Server Validation**: All access keys validated server-side

### Default Test Configuration

For development and testing:

```bash
RECEPTIONIST_KEY=111        # Simple keys for testing
OBSERVER_KEY=333           
SAFETY_KEY=222             
```

**Production**: Use strong, unique keys for each role.

---

<a id="development-guide"></a>
## 🛠️ Development Guide

### Development vs Production

**Development Features:**
- **Short Races**: 60 seconds instead of 10 minutes
- **Detailed Logging**: All operations logged to `data/log.log`
- **Test Data**: Option to start with sample sessions
- **Debug Info**: Comprehensive error information

**Production Features:**
- **Full Races**: 10-minute race duration
- **Silent Operation**: Clean terminal output
- **Optimized Performance**: Reduced logging overhead
- **Stable Configuration**: Production-ready settings

### Development Commands

```bash
# ⚠️  DESTRUCTIVE: Start with fresh test data (asks for confirmation)
npm run "dev testData"

# 🔒 SAFE: Development mode with existing data preserved
npm run dev

# 🏁 Production mode
npm start

# Check logs (development mode only)
tail -f data/log.log
```

### 🛡️ Data Safety Features

**Test Data Protection:**
- `npm run "dev testData"` requires **explicit confirmation**
- **Clear warning** about data deletion before proceeding
- **Automatic fallback** to regular dev mode if cancelled
- **Visual indicators** during reset process

### Data Persistence

**Session Storage:**
- Location: `data/sessions.json`
- Format: Structured JSON with drivers, cars, race state
- Backup: Automatic recovery after server restart

**Race Recovery:**
- Active races continue after server restart
- Timing and lap data preserved
- All interfaces notified of restored state

---

<a id="technical-architecture"></a>
## 🏗️ Technical Architecture

### System Overview

The system features a **modular architecture** with clean separation of concerns:

```
┌─────────────────────────────────────────┐
│            Frontend Interfaces          │
├─────────────┬─────────────┬─────────────┤
│ Management  │   Public    │   Control   │
│ Interfaces  │  Displays   │   Center    │
│ (Auth Req.) │ (No Auth)   │ (Dashboard) │
└─────────────┴─────────────┴─────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│         Real-time Communication         │
│            (Socket.IO)                  │
└─────────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│           Backend Services              │
├─────────────────────────────────────────┤
│ • Controllers (Business Logic)          │
│ • Services (Data, Socket, Logging)      │
│ • Routes (HTTP Handlers)               │
│ • Models (Data Structures)             │
└─────────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────────┐
│           Data Storage                  │
│     JSON Files + In-Memory State       │
└─────────────────────────────────────────┘
```

### Technology Stack

**Backend:**
- **Node.js & Express.js**: Server and API
- **Socket.IO**: Real-time communication
- **JSON Files**: Data persistence
- **Environment Variables**: Configuration

**Frontend:**
- **Vanilla JavaScript**: Client-side logic
- **WebSocket**: Real-time updates
- **Responsive CSS**: Mobile-friendly design
- **HTML5**: Interface templates

### Project Structure

```
race-track/
├── server.js                    # Main entry point
├── package.json                 # Dependencies & scripts
├── .env example                 # Configuration template
├── backend/
│   ├── config/                  # Environment & constants
│   ├── controllers/             # Business logic
│   ├── routes/                  # HTTP endpoints
│   ├── services/                # Core services
│   └── models/                  # Data structures
├── public/
│   ├── interfaces/              # HTML pages
│   ├── js/                      # Client-side code
│   └── styles.css               # Shared styling
└── data/
    ├── sessions.json            # Session data
    └── log.log                  # Development logs
```

🏗️ **For detailed architecture documentation, see [ARCHITECTURE.md](docs/ARCHITECTURE.md)**

---

<a id="customization"></a>
## 🔧 Customization

### Race Configuration

Edit `backend/config/constants.js`:

```javascript
const RACE_TIMING = {
    DEVELOPMENT_DURATION: 60000,    // 1 minute for testing
    PRODUCTION_DURATION: 600000,    // 10 minutes for races
};

AVAILABLE_CARS: [1, 2, 3, 4, 5, 6, 7, 8]  // Car numbers
```

### Interface Customization

- **HTML Templates**: Modify `public/interfaces/*.html`
- **Client Logic**: Update `public/js/*.js`
- **Styling**: Customize `public/styles.css`
- **Branding**: Change titles, colors, logos in templates

### Access Keys

Production deployment should use strong keys:

```bash
# Generate strong keys for production
RECEPTIONIST_KEY=racetrack_front_desk_2024_secure
SAFETY_KEY=safety_officer_control_panel_key
OBSERVER_KEY=lap_timing_observer_access_key
```

---

## 📚 Documentation & Support

### Complete Guides
- **[INSTALLATION.md](docs/INSTALLATION.md)** - Step-by-step setup for beginners
- **[ARCHITECTURE.md](docs/ARCHITECTURE.md)** - Technical details and relationships

### Troubleshooting

**Common Issues:**

**Authentication not working:**
- Check `.env` file exists and has correct keys
- Restart server after changing `.env` file
- Verify you're using the right key for each interface

**Can't connect to interfaces:**
- Ensure server is running on `http://localhost:3000`
- Check firewall settings if accessing remotely
- Try different browser if issues persist

**Race data not saving:**
- Check `data/` directory permissions
- Ensure sufficient disk space
- Check console for error messages

**Need help?** Check the complete guides above or review error messages in the terminal.

---

**🏁 Built for professional race track operations with real-time coordination and spectator engagement! 🏁**