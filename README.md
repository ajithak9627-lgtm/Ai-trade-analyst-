# Ai-trade-analyst-# AI Trade Analyst (Phase 1)

AI Trade Analyst is a self-hosted full-stack web application designed to help traders analyze chart patterns, calculate precise position sizing, and evaluate risk dynamics using Claude AI models. The interface and AI reports fully support both **English** and **Tamil**.

> ⚠️ **Note:** This project is currently in a pre-deployment/untested sandbox phase. Core algorithmic rules (server-side risk maths and trade signal validation) have been verified against hand calculations, but full runtime integration testing is pending.

---

## 🛡️ Core Features & Safety Architecture

- **Split Analysis UI:** Chart facts identified by the AI are explicitly separated from speculative scenarios to prevent data confusion.
- **Server-Side Validation:** 
  - If Entry, Stop-Loss (SL), and Take-Profit (TP) levels do not form a logical trade setup, the signal is automatically overridden and forced to `WAIT`.
  - Risk-to-Reward (R:R) ratios and position-sizes are strictly computed via deterministic server algorithms, not estimated by the AI.
- **Strict Security:** API Keys reside entirely on the backend environment variables. Frontend image uploads are validated via binary file signatures/content parsing, not just filename extensions.
- **No False Certainty:** Confidence ratings are constrained to categorical labels (`Low`, `Medium`, `High`) paired with qualitative logic—never numerical percentages.
- **Regulatory Gatekeeping:** a mandatory risk warning modal must be acknowledged by the user before any analysis results are displayed.
- **Cost-Optimized Defaults:** Configured to run on `claude-haiku-5-5` by default to minimize API overhead, with an optional toggle for `claude-sonnet-5-5` for advanced visual parsing.

---

## 📁 Repository Structure & Directory Map

Ensure your local files match the target directory layout specified below before running the installation steps:

```text
ai-trade-analyst/
├── server/
│   ├── .env.example
│   ├── package.json
│   └── app.js             # Contains validation engine & risk math overrides
└── client/
    ├── package.json
    ├── src/
    │   ├── main.jsx
    │   └── components/    # Contains all 6 screens (Home, Upload, Result, Risk, History, Settings)
    └── public/
```

---

## 💻 Installation & Setup (Windows 10)

Follow these sequential steps to configure and run the application locally:

### 1. Prerequisites
Download and install **Node.js LTS** (Long Term Support) from the official website. Verify the installation in your Command Prompt/PowerShell:
```cmd
node -v
npm -v
```

### 2. Configure Environment Variables
Navigate to the `server` directory, copy the template configuration file, and append your credentials:
1. Copy `server/.env.example` and rename the copy to `.env`.
2. Open the new `.env` file and insert your Anthropic API Key:
   ```env
   ANTHROPIC_API_KEY=your_actual_api_key_here
   CLAUDE_MODEL=claude-haiku-5-5
   PORT=5000
   ```
   *(Note: You can switch `CLAUDE_MODEL` to `claude-sonnet-5-5` inside this file if you require more rigorous chart reading).*

### 3. Install Dependencies
Open two distinct terminal windows to install dependencies for both the backend and frontend modules:

**Terminal 1 (Backend Server):**
```cmd
cd server
npm install
```

**Terminal 2 (Frontend Client):**
```cmd
cd client
npm install
```

### 4. Running the Application

Execution must happen in parallel across your separate terminal instances:

- **Start the Server:** In Terminal 1 (`server` directory), execute:
  ```cmd
  npm start
  ```
- **Start the Client:** In Terminal 2 (`client` directory), execute:
  ```cmd
  npm run dev
  ```

Once both instances are running, open your Google Chrome browser and navigate to:
🔗 **`http://localhost:5173`**

---

## 🔮 Phase 2 Roadmap: Live Market Data
Live streaming market data integration is slated for Phase 2. Because free-tier financial data feeds typically enforce a time delay, the user interface is pre-built to append a prominent **Live** or **Delayed** tag alongside a precise data timestamp. 

If you already possess a license or developer API key for a specific data aggregator (e.g., *Alpha Vantage, Twelvedata, Polygon.io, or Kite Connect*), please forward the provider requirements to integrate the live feed module.