# ⚙️ CPU Scheduling Simulator

A full-stack web application to **simulate and visualize** 4 classic CPU scheduling algorithms with interactive Gantt charts, per-process statistics, and average performance metrics.

![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat&logo=node.js&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=flat&logo=react&logoColor=white)
![Express](https://img.shields.io/badge/Express-4.x-000000?style=flat&logo=express&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat)

---

## 🖥️ Live Preview

> Run locally — see [Setup](#-setup--running) below.

The app features a dark-themed dashboard with:
- Color-coded **Gantt chart** visualization
- **Process statistics table** (waiting time, turnaround time)
- **Average metrics** cards
- Algorithm switcher with instant context

---

## 🧠 Algorithms

| Algorithm | Type | Key Idea |
|-----------|------|----------|
| **First Come First Serve (FCFS)** | Non-preemptive | Processes run in order of arrival |
| **Shortest Job First (SJF)** | Non-preemptive | Shortest burst time runs next |
| **Priority Scheduling** | Non-preemptive | Lower priority number = runs first |
| **Round Robin (RR)** | Preemptive | Each process gets a fixed time quantum |

---

## 📁 Project Structure

```
cpu-scheduler/
├── backend/
│   ├── server.js        ← Express REST API (all 4 algorithms)
│   └── package.json
├── frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── App.js       ← Main React component + UI
│   │   ├── App.css      ← Styling (dark theme)
│   │   └── index.js     ← React entry point
│   └── package.json
└── README.md
```

---

## ⚙️ Prerequisites

| Tool | Version | Download |
|------|---------|----------|
| Node.js | v16 or higher | https://nodejs.org |
| npm | v8 or higher | Comes with Node.js |

Verify installation:
```bash
node -v
npm -v
```

---

## 🚀 Setup & Running

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/cpu-scheduler.git
cd cpu-scheduler
```

### 2. Start the Backend

```bash
cd backend
npm install
npm start
```

Expected output:
```
✅  CPU Scheduler API running on http://localhost:5000
```

> Keep this terminal open.

### 3. Start the Frontend

Open a **new terminal**:

```bash
cd frontend
npm install
npm start
```

The app will open automatically at **http://localhost:3000**

---

## 🎮 How to Use

1. **Select an algorithm** from the tab bar at the top
2. **Edit the process table** — set names, burst times, and arrival times
3. For **Priority scheduling** → a Priority column appears (1 = highest priority)
4. For **Round Robin** → set the Time Quantum value in milliseconds
5. Click **▶ Simulate** to run the selected algorithm
6. View the **Gantt Chart**, **statistics table**, and **average metrics**
7. Click **↺ Reset** to restore default values

---

## 🔌 API Reference

Base URL: `http://localhost:5000`

### `POST /fcfs` — First Come First Serve

```json
{
  "processes": [
    { "name": "P1", "burst": 6, "arrival": 0 },
    { "name": "P2", "burst": 4, "arrival": 1 }
  ]
}
```

### `POST /sjf` — Shortest Job First

Same request body as FCFS.

### `POST /priority` — Priority Scheduling

```json
{
  "processes": [
    { "name": "P1", "burst": 6, "arrival": 0, "priority": 2 },
    { "name": "P2", "burst": 4, "arrival": 1, "priority": 1 }
  ]
}
```

### `POST /rr` — Round Robin

```json
{
  "quantum": 2,
  "processes": [
    { "name": "P1", "burst": 6, "arrival": 0 },
    { "name": "P2", "burst": 4, "arrival": 1 }
  ]
}
```

### Response Format (all endpoints)

```json
{
  "gantt": [
    { "process": "P1", "start": 0, "end": 6, "waitingTime": 0, "turnaroundTime": 6 }
  ],
  "stats": [ ... ],
  "avgWaitingTime": 2.5,
  "avgTurnaroundTime": 6.5
}
```

---

## 🛠️ Development Mode

Backend with auto-restart on file changes:
```bash
cd backend
npm run dev
```

Frontend already has hot reload via `npm start`.

---

## ❗ Troubleshooting

| Problem | Solution |
|---------|----------|
| `Cannot connect to backend` | Make sure backend is running on port 5000 |
| `Port 3000 already in use` | Run `npx kill-port 3000` then retry |
| `Port 5000 already in use` | Run `npx kill-port 5000` then retry |
| `npm install fails` | Try `npm install --legacy-peer-deps` |
| `node: command not found` | Install Node.js from https://nodejs.org |
| Blank screen in browser | Check browser console for errors (F12) |

---

## 📦 Tech Stack

**Backend**
- [Node.js](https://nodejs.org) — Runtime
- [Express](https://expressjs.com) — REST API framework
- [CORS](https://github.com/expressjs/cors) — Cross-origin requests

**Frontend**
- [React 18](https://reactjs.org) — UI framework
- [Axios](https://axios-http.com) — HTTP client
- [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) — Monospace font
- [Inter](https://fonts.google.com/specimen/Inter) — UI font

---

## 📝 Algorithm Notes

- **FCFS** — Simple but can cause the "convoy effect" where short processes wait behind long ones
- **SJF** — Optimal average waiting time but requires knowing burst time in advance; can cause starvation
- **Priority** — Lower number means higher priority; can cause starvation of low-priority processes
- **Round Robin** — Fair and starvation-free; performance depends heavily on the chosen quantum size

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

Made with ❤️ using React + Express
