<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>FIFA World Cup 2026 – Pro Simulator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg-main: #020617;
      --bg-panel: #020617;
      --bg-panel-soft: rgba(9, 9, 18, 0.96);
      --accent-1: #22d3ee;
      --accent-2: #a855f7;
      --accent-3: #22c55e;
      --border-soft: #1f2937;
      --text-main: #f9fafb;
      --text-soft: #9ca3af;
      --text-muted: #6b7280;
      --danger: #ef4444;
      --radius-lg: 20px;
      --radius-md: 12px;
      --shadow-strong: 0 22px 70px rgba(15, 23, 42, 0.95);
    }

    * {
      box-sizing: border-box;
      font-family: "Inter", system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      padding: 0;
      min-height: 100vh;
      background:
        radial-gradient(circle at top left, rgba(34, 211, 238, 0.16), transparent 55%),
        radial-gradient(circle at bottom right, rgba(168, 85, 247, 0.2), transparent 60%),
        var(--bg-main);
      color: var(--text-main);
      display: flex;
    }

    .app {
      width: 100%;
      max-width: 1500px;
      margin: 0 auto;
      padding: 18px 16px 26px;
    }

    header {
      display: flex;
      flex-wrap: wrap;
      align-items: flex-start;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 16px;
      animation: fadeInDown 0.6s ease both;
    }

    h1 {
      margin: 0;
      font-size: 1.7rem;
      letter-spacing: 0.03em;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .tagline {
      font-size: 0.86rem;
      color: var(--text-soft);
      max-width: 460px;
      margin-top: 4px;
    }

    .pill {
      border-radius: 999px;
      padding: 4px 11px;
      font-size: 0.7rem;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      border: 1px solid rgba(148, 163, 184, 0.7);
      background: rgba(15, 23, 42, 0.9);
      color: #e5e7eb;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .pill span.dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--accent-3);
      box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.22);
    }

    .step-indicator {
      margin-top: 4px;
      font-size: 0.75rem;
      color: var(--text-muted);
    }

    .step-indicator span.current {
      color: var(--accent-1);
      font-weight: 500;
    }

    /* Views */

    .view {
      display: none;
    }
    .view.active {
      display: block;
    }

    .panel {
      background:
        radial-gradient(circle at top, rgba(148, 163, 184, 0.22), transparent 60%),
        var(--bg-panel-soft);
      border-radius: var(--radius-lg);
      padding: 14px 14px 16px;
      border: 1px solid rgba(30, 64, 175, 0.65);
      box-shadow:
        var(--shadow-strong),
        0 0 0 1px rgba(15, 23, 42, 0.9);
      backdrop-filter: blur(16px);
      animation: floatUp 0.6s ease both;
    }

    .panel-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 10px;
      gap: 10px;
    }

    .panel-header h2 {
      margin: 0;
      font-size: 1rem;
    }

    .badge {
      font-size: 0.7rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: #e0f2fe;
      background: linear-gradient(135deg, rgba(56, 189, 248, 0.25), rgba(168, 85, 247, 0.25));
      padding: 3px 9px;
      border-radius: 999px;
      border: 1px solid rgba(96, 165, 250, 0.8);
      white-space: nowrap;
    }

    .help-text {
      font-size: 0.78rem;
      color: var(--text-soft);
      margin-bottom: 8px;
    }

    /* GROUP VIEW */

    #view-groups .layout-groups {
      display: grid;
      grid-template-columns: minmax(0, 1.2fr) minmax(260px, 0.9fr);
      gap: 18px;
    }

    @media (max-width: 980px) {
      #view-groups .layout-groups {
        grid-template-columns: 1fr;
      }
    }

    .groups-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
      gap: 10px;
      max-height: 480px;
      overflow: auto;
      padding-right: 2px;
    }

    .group-card {
      background:
        radial-gradient(circle at top left, rgba(56, 189, 248, 0.3), transparent 60%),
        #020617;
      border-radius: 16px;
      border: 1px solid rgba(31, 41, 55, 0.95);
      padding: 8px 8px 7px;
      box-shadow: 0 10px 24px rgba(15, 23, 42, 0.9);
      animation: fadeIn 0.4s ease both;
    }

    .group-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }

    .group-name {
      font-size: 0.9rem;
      font-weight: 600;
    }

    .group-sub {
      font-size: 0.7rem;
      color: var(--text-soft);
    }

    .team-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 4px;
      padding: 4px 6px;
      border-radius: 10px;
      border: 1px solid rgba(31, 41, 55, 0.9);
      background: linear-gradient(135deg, #020617, #020617);
      margin-bottom: 4px;
      font-size: 0.78rem;
      transition: border 0.15s, background 0.15s, transform 0.1s;
    }

    .team-row:nth-child(2) {
      border-color: rgba(34, 197, 94, 0.85);
      background:
        radial-gradient(circle at left, rgba(34, 197, 94, 0.18), transparent 65%),
        #020617;
    }

    .team-row:hover {
      border-color: rgba(56, 189, 248, 0.95);
      transform: translateY(-1px);
    }

    .team-row-left {
      display: flex;
      align-items: center;
      gap: 7px;
      overflow: hidden;
    }

    .flag-wrapper {
      width: 28px;
      height: 20px;
      border-radius: 4px;
      overflow: hidden;
      border: 1px solid rgba(31, 41, 55, 0.9);
      box-shadow: 0 0 0 3px rgba(15, 23, 42, 1);
      display: flex;
      align-items: center;
      justify-content: center;
      background: #020617;
    }

    .flag-img {
      width: 100%;
      height: auto;
      display: block;
    }

    .flag-fallback {
      font-size: 0.65rem;
      color: var(--text-soft);
    }

    .team-name {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .place-pill {
      font-size: 0.65rem;
      padding: 2px 7px;
      border-radius: 999px;
      border: 1px solid rgba(55, 65, 81, 0.95);
      color: var(--text-soft);
      white-space: nowrap;
      background: rgba(15, 23, 42, 0.95);
    }

    .team-controls {
      display: flex;
      flex-direction: column;
      gap: 3px;
    }

    .icon-btn {
      border-radius: 6px;
      border: 1px solid rgba(31, 41, 55, 0.98);
      background: rgba(15, 23, 42, 0.96);
      padding: 1px 4px;
      cursor: pointer;
      font-size: 0.7rem;
      color: var(--text-soft);
      line-height: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.12s, transform 0.08s, border 0.12s, color 0.12s;
    }

    .icon-btn:hover:not(:disabled) {
      background: rgba(56, 189, 248, 0.95);
      border-color: rgba(191, 219, 254, 1);
      color: #020617;
      transform: translateY(-0.5px);
    }

    .icon-btn:disabled {
      opacity: 0.25;
      cursor: default;
    }

    .btn-row {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 8px 0 10px;
    }

    button.main-btn {
      border-radius: 999px;
      padding: 7px 14px;
      font-size: 0.8rem;
      border: none;
      cursor: pointer;
      background: linear-gradient(135deg, var(--accent-1), var(--accent-2));
      color: white;
      font-weight: 500;
      box-shadow: var(--shadow-strong);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: transform 0.1s ease, box-shadow 0.12s ease, filter 0.12s ease;
    }

    button.main-btn:hover {
      transform: translateY(-1px);
      filter: brightness(1.04);
      box-shadow: 0 18px 40px rgba(15, 23, 42, 1);
    }

    button.main-btn:active {
      transform: translateY(0);
      box-shadow: 0 10px 22px rgba(15, 23, 42, 1);
    }

    button.outline-btn {
      border-radius: 999px;
      padding: 6px 12px;
      font-size: 0.8rem;
      cursor: pointer;
      background: rgba(15, 23, 42, 0.96);
      border: 1px solid rgba(75, 85, 99, 0.95);
      color: #e5e7eb;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: background 0.12s, transform 0.1s, border 0.12s;
    }

    button.outline-btn:hover {
      background: rgba(31, 41, 55, 0.98);
      transform: translateY(-1px);
      border-color: rgba(148, 163, 184, 0.95);
    }

    /* bigger third-place panel */
    .thirds-list {
      max-height: 340px;      /* <-- made taller */
      overflow: auto;
      padding: 7px;
      background: rgba(15, 23, 42, 0.97);
      border-radius: 14px;
      border: 1px solid rgba(31, 41, 55, 0.98);
      font-size: 0.8rem;
    }

    .third-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 8px;
      margin-bottom: 5px;
    }

    .third-item label {
      display: flex;
      align-items: center;
      gap: 7px;
      cursor: pointer;
    }

    .third-item small {
      color: var(--text-soft);
      white-space: nowrap;
    }

    .note {
      font-size: 0.72rem;
      color: var(--text-muted);
      margin-top: 4px;
    }

    /* KNOCKOUT VIEW */

    #view-knockout {
      margin-top: 6px;
    }

    .knockout-layout {
      display: grid;
      grid-template-columns: minmax(0, 2fr) minmax(270px, 0.9fr);
      gap: 16px;
    }

    @media (max-width: 1100px) {
      .knockout-layout {
        grid-template-columns: 1fr;
      }
    }

    .back-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
      gap: 8px;
    }

    .back-left {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 0.8rem;
      color: var(--text-soft);
    }

    .back-left span.step-label {
      text-transform: uppercase;
      letter-spacing: 0.1em;
      font-size: 0.72rem;
      color: var(--accent-1);
    }

    .link-btn {
      border-radius: 999px;
      padding: 5px 11px;
      font-size: 0.78rem;
      border: 1px solid rgba(148, 163, 184, 0.9);
      background: rgba(15, 23, 42, 0.96);
      color: #e5e7eb;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: background 0.12s, transform 0.08s, border 0.12s;
    }

    .link-btn:hover {
      background: rgba(30, 64, 175, 0.9);
      border-color: rgba(191, 219, 254, 1);
      transform: translateY(-0.5px);
    }

    .champion-banner {
      background:
        radial-gradient(circle at top, rgba(250, 204, 21, 0.35), transparent 60%),
        linear-gradient(145deg, #020617, #020617);
      border-radius: 16px;
      padding: 10px 12px;
      border: 1px solid rgba(250, 204, 21, 0.85);
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      box-shadow:
        0 10px 30px rgba(15, 23, 42, 0.95),
        0 0 0 1px rgba(15, 23, 42, 0.9);
    }

    .champion-label {
      font-size: 0.75rem;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      color: #fef3c7;
    }

    .champion-name {
      font-size: 1.12rem;
      font-weight: 700;
      color: #facc15;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .champion-placeholder {
      font-size: 0.85rem;
      color: #e5e7eb;
    }

    .trophy-emoji {
      font-size: 1.6rem;
      animation: pulseTrophy 1.2s ease-in-out infinite;
    }

    .champion-banner.glow {
      animation: championGlow 1.6s ease-in-out infinite;
    }

    .bracket {
      display: grid;
      grid-template-columns: repeat(5, minmax(0, 1fr));
      gap: 10px;
      overflow-x: auto;
      padding-bottom: 4px;
    }

    .round-column {
      background: rgba(15, 23, 42, 0.98);
      border-radius: 16px;
      border: 1px solid rgba(31, 41, 55, 0.98);
      padding: 8px;
      min-width: 190px;
      box-shadow: 0 14px 28px rgba(15, 23, 42, 0.95);
      animation: fadeIn 0.4s ease both;
    }

    .round-title {
      font-size: 0.78rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.09em;
      color: var(--text-soft);
      margin-bottom: 6px;
    }

    .match {
      margin-bottom: 8px;
      padding-bottom: 6px;
      border-bottom: 1px dashed rgba(31, 41, 55, 0.95);
    }

    .match:last-child {
      border-bottom: none;
      margin-bottom: 0;
    }

    .team-line {
      display: flex;
      align-items: center;
      gap: 5px;
      margin-bottom: 3px;
    }

    .team-btn {
      flex: 1;
      text-align: left;
      padding: 5px 7px;
      border-radius: 9px;
      font-size: 0.78rem;
      background: rgba(15, 23, 42, 0.96);
      border: 1px solid rgba(31, 41, 55, 0.98);
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      cursor: pointer;
      transition: background 0.12s, border 0.12s, transform 0.08s;
      color: #e5e7eb;
    }

    .team-btn-inner {
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .team-btn .flag-wrapper {
      width: 24px;
      height: 16px;
      box-shadow: 0 0 0 2px rgba(15, 23, 42, 1);
    }

    .team-btn.filled {
      border-color: rgba(55, 65, 81, 0.98);
    }

    .team-btn.winner {
      border-color: rgba(34, 197, 94, 0.98);
      background:
        radial-gradient(circle at left, rgba(34, 197, 94, 0.2), transparent 80%),
        rgba(15, 23, 42, 0.98);
      box-shadow: 0 0 0 1px rgba(34, 197, 94, 0.4);
    }

    .team-btn:disabled {
      opacity: 0.50;
      cursor: default;
    }

    .team-btn:hover:not(:disabled) {
      background: rgba(56, 189, 248, 0.9);
      border-color: rgba(191, 219, 254, 1);
      transform: translateY(-0.5px);
      color: #020617;
    }

    .score-input {
      width: 45px;
      padding: 4px;
      border-radius: 8px;
      border: 1px solid rgba(55, 65, 81, 0.98);
      background: rgba(15, 23, 42, 0.96);
      color: #e5e7eb;
      font-size: 0.78rem;
      text-align: center;
      outline: none;
      transition: border 0.12s, box-shadow 0.12s, background 0.12s;
    }

    .score-input:focus {
      border-color: var(--accent-1);
      background: #020617;
      box-shadow: 0 0 0 1px rgba(34, 211, 238, 0.4);
    }

    .score-input::-webkit-outer-spin-button,
    .score-input::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }

    .score-input[type=number] {
      -moz-appearance: textfield;
    }

    .match-note {
      font-size: 0.68rem;
      color: var(--text-muted);
      margin-top: 2px;
    }

    .footer-note {
      margin-top: 6px;
      font-size: 0.72rem;
      color: var(--text-muted);
    }

    .footer-note span {
      color: var(--accent-2);
    }

    /* PREDICTION PANEL */

    .prediction-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 6px;
    }

    .prediction-header h3 {
      margin: 0;
      font-size: 0.95rem;
    }

    .prediction-help {
      font-size: 0.76rem;
      color: var(--text-soft);
      margin-bottom: 8px;
    }

    .prediction-form {
      display: flex;
      gap: 6px;
      margin-bottom: 8px;
    }

    .prediction-form input {
      flex: 1;
      border-radius: 999px;
      border: 1px solid rgba(55, 65, 81, 0.95);
      background: rgba(15, 23, 42, 0.96);
      color: #e5e7eb;
      font-size: 0.8rem;
      padding: 6px 9px;
      outline: none;
      transition: border 0.12s, box-shadow 0.12s, background 0.12s;
    }

    .prediction-form input:focus {
      border-color: var(--accent-1);
      box-shadow: 0 0 0 1px rgba(34, 211, 238, 0.4);
      background: #020617;
    }

    .prediction-save-btn {
      border-radius: 999px;
      border: none;
      padding: 6px 10px;
      font-size: 0.78rem;
      cursor: pointer;
      background: linear-gradient(135deg, var(--accent-2), var(--accent-3));
      color: #f9fafb;
      white-space: nowrap;
      display: inline-flex;
      align-items: center;
      gap: 5px;
      transition: transform 0.1s, box-shadow 0.12s, filter 0.12s;
      box-shadow: 0 10px 22px rgba(15, 23, 42, 0.9);
    }

    .prediction-save-btn:hover {
      transform: translateY(-1px);
      filter: brightness(1.05);
      box-shadow: 0 14px 30px rgba(15, 23, 42, 1);
    }

    .prediction-save-btn:active {
      transform: translateY(0);
      box-shadow: 0 8px 18px rgba(15, 23, 42, 1);
    }

    .prediction-status {
      font-size: 0.75rem;
      margin-bottom: 6px;
      min-height: 16px;
    }

    .prediction-status.ok {
      color: #bbf7d0;
    }

    .prediction-status.err {
      color: #fecaca;
    }

    .prediction-list-empty {
      font-size: 0.76rem;
      color: var(--text-muted);
    }

    .prediction-list {
      max-height: 260px;
      overflow: auto;
      padding-right: 2px;
    }

    .prediction-card {
      border-radius: 12px;
      border: 1px solid rgba(31, 41, 55, 0.98);
      background: rgba(15, 23, 42, 0.97);
      padding: 6px 7px;
      margin-bottom: 6px;
      font-size: 0.78rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 6px;
    }

    .prediction-main {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }

    .prediction-name {
      font-weight: 500;
    }

    .prediction-winner {
      font-size: 0.78rem;
      color: #e5e7eb;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .prediction-meta {
      font-size: 0.7rem;
      color: var(--text-muted);
      white-space: nowrap;
    }

    /* ANIMATIONS */

    @keyframes fadeInDown {
      from { opacity: 0; transform: translateY(-6px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(4px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @keyframes floatUp {
      from { opacity: 0; transform: translateY(10px) scale(0.98); }
      to   { opacity: 1; transform: translateY(0) scale(1); }
    }

    @keyframes championGlow {
      0% {
        box-shadow:
          0 10px 30px rgba(15, 23, 42, 0.9),
          0 0 0 0 rgba(250, 204, 21, 0.3);
      }
      50% {
        box-shadow:
          0 16px 40px rgba(15, 23, 42, 0.95),
          0 0 0 6px rgba(250, 204, 21, 0.16);
      }
      100% {
        box-shadow:
          0 10px 30px rgba(15, 23, 42, 0.9),
          0 0 0 0 rgba(250, 204, 21, 0.3);
      }
    }

    @keyframes pulseTrophy {
      0%,100% { transform: translateY(0) scale(1); }
      50% { transform: translateY(-1px) scale(1.04); }
    }

    @media (max-width: 600px) {
      h1 { font-size: 1.45rem; }
      .round-column { min-width: 170px; }
    }
  </style>
</head>

<body>
  <div class="app">
    <header>
      <div>
        <h1>FIFA World Cup 2026 – Pro Simulator</h1>
        <div class="tagline">
          Step 1: arrange the official-style groups A–L. Step 2: open the
          knockout view in a clean separate screen, enter scores and click winners.
          You can also save your prediction with your name.
        </div>
        <div class="step-indicator">
          <span class="current">Step 1:</span> Group stage ·
          <span>Step 2:</span> Knockout & predictions
        </div>
      </div>
      <div class="pill">
        <span class="dot"></span>
        48 Teams · 12 Groups · 32 Knockout
      </div>
    </header>

    <!-- GROUPS VIEW -->
    <section id="view-groups" class="view active">
      <div class="layout-groups">
        <section class="panel">
          <div class="panel-header">
            <h2>Group Stage (A–L)</h2>
            <span class="badge">Step 1 – Rank tables</span>
          </div>
          <p class="help-text">
            Use ▲ / ▼ to move teams in each group. The order is the final ranking:
            <b>top row = 1st place</b>, then 2nd, 3rd, 4th.
          </p>
          <div class="groups-grid" id="groupsContainer"></div>

          <div class="btn-row">
            <button class="main-btn" id="confirmGroupsBtn">
              <span>Step 1: Confirm Group Standings</span>
            </button>
            <button class="outline-btn" id="resetAllBtn">
              <span>Reset All</span>
            </button>
          </div>
        </section>

        <section class="panel">
          <div class="panel-header">
            <h2>Third-place qualifiers</h2>
            <span class="badge">Step 1.5 – Pick 8</span>
          </div>
          <p class="help-text">
            After confirming, all 3rd-place teams (from groups A–L) appear here with flags.
            Choose exactly <b>8</b> to complete the 32-team knockout.
          </p>

          <div class="thirds-list" id="thirdsList">
            <span style="font-size: 0.8rem; color:#6b7280;">
              Confirm groups first to show all 3rd-place teams.
            </span>
          </div>

          <div class="btn-row">
            <button class="main-btn" id="generateKnockoutBtn">
              <span>Step 2: Open Knockout View</span>
            </button>
          </div>
          <p class="note">
            24 teams auto-qualify as group winners & runners-up (12 × 2).
            You add 8 more from the 3rd-place list → total 32 for the knockout.
          </p>
        </section>
      </div>
    </section>

    <!-- KNOCKOUT VIEW -->
    <section id="view-knockout" class="view">
      <div class="back-row">
        <div class="back-left">
          <span class="step-label">Step 2 · Knockout</span>
          <span>Scores + winners + saved predictions</span>
        </div>
        <button class="link-btn" id="backToGroupsBtn">
          ← Edit group stage
        </button>
      </div>

      <div class="knockout-layout">
        <section class="panel">
          <div class="panel-header">
            <h2>Knockout Bracket</h2>
            <span class="badge">Round of 32 → Final</span>
          </div>

          <div class="champion-banner" id="championBanner">
            <div>
              <div class="champion-label">Champion</div>
              <div id="championName" class="champion-placeholder">
                Generate the bracket and then enter scores / click winners
                until your champion appears here.
              </div>
            </div>
            <div class="trophy-emoji">🏆</div>
          </div>

          <div class="bracket" id="bracketContainer"></div>

          <p class="footer-note">
            • Enter <b>scores</b> – higher score advances automatically.
            • For a draw, click the team you want to win on penalties.
            • Seeding uses a simple <span>1 vs 32, 2 vs 31</span> style (for fun, not official).
          </p>
        </section>

        <section class="panel">
          <div class="prediction-header">
            <h3>Saved predictions</h3>
            <span class="badge" style="font-size:0.68rem;">Local leaderboard</span>
          </div>
          <p class="prediction-help">
            When a champion is decided, enter your name or nickname and save your pick.
            Anyone using this browser can see all saved winners (stored in this device's memory).
          </p>

          <div class="prediction-form">
            <input id="userNameInput" type="text" maxlength="40"
                   placeholder="Your name or nickname" />
            <button class="prediction-save-btn" id="savePredictionBtn">
              💾 Save winner
            </button>
          </div>

          <div class="prediction-status" id="predictionStatus"></div>

          <div id="predictionListContainer">
            <div class="prediction-list-empty">
              No predictions yet. Play the knockout and save your champion!
            </div>
          </div>
        </section>
      </div>
    </section>
  </div>

  <script>
    // ---------- GROUP DATA ----------
    const OFFICIAL_GROUPS = {
      "A": ["Mexico", "South Africa", "South Korea", "European Playoff D"],
      "B": ["Canada", "European Playoff A", "Qatar", "Switzerland"],
      "C": ["Brazil", "Morocco", "Haiti", "Scotland"],
      "D": ["United States", "Paraguay", "Australia", "European Playoff C"],
      "E": ["Germany", "Curaçao", "Ivory Coast", "Ecuador"],
      "F": ["Netherlands", "Japan", "European Playoff B", "Tunisia"],
      "G": ["Belgium", "Egypt", "Iran", "New Zealand"],
      "H": ["Spain", "Cape Verde", "Saudi Arabia", "Uruguay"],
      "I": ["France", "Senegal", "FIFA Intercontinental Playoff 2", "Norway"],
      "J": ["Argentina", "Algeria", "Austria", "Jordan"],
      "K": ["Portugal", "FIFA Intercontinental Playoff 1", "Uzbekistan", "Colombia"],
      "L": ["England", "Croatia", "Ghana", "Panama"],
    };

    const FLAG_CODES = {
      "Mexico": "mx",
      "South Africa": "za",
      "South Korea": "kr",
      "Canada": "ca",
      "Qatar": "qa",
      "Switzerland": "ch",
      "Brazil": "br",
      "Morocco": "ma",
      "Haiti": "ht",
      "Scotland": "gb-sct",
      "United States": "us",
      "Paraguay": "py",
      "Australia": "au",
      "Germany": "de",
      "Curaçao": "cw",
      "Curacao": "cw",
      "Ivory Coast": "ci",
      "Côte d'Ivoire": "ci",
      "Ecuador": "ec",
      "Netherlands": "nl",
      "Japan": "jp",
      "Tunisia": "tn",
      "Belgium": "be",
      "Egypt": "eg",
      "Iran": "ir",
      "New Zealand": "nz",
      "Spain": "es",
      "Cape Verde": "cv",
      "Saudi Arabia": "sa",
      "Uruguay": "uy",
      "France": "fr",
      "Senegal": "sn",
      "Norway": "no",
      "Argentina": "ar",
      "Algeria": "dz",
      "Austria": "at",
      "Jordan": "jo",
      "Portugal": "pt",
      "Uzbekistan": "uz",
      "Colombia": "co",
      "England": "gb-eng",
      "Croatia": "hr",
      "Ghana": "gh",
      "Panama": "pa",
    };

    function getFlagCode(name) {
      if (!name) return null;
      const clean = name.split(" (")[0].trim();
      if (FLAG_CODES[clean]) return FLAG_CODES[clean];
      if (clean.startsWith("European Playoff")) return "eu";
      if (clean.startsWith("FIFA Intercontinental")) return "un";
      return null;
    }

    function createFlagElement(teamName, small = false) {
      const wrap = document.createElement("div");
      wrap.className = "flag-wrapper";
      if (small) wrap.style.boxShadow = "0 0 0 2px rgba(15,23,42,1)";

      const code = getFlagCode(teamName);
      if (code) {
        const img = document.createElement("img");
        img.className = "flag-img";
        img.src = `https://flagcdn.com/24x18/${code}.png`;
        img.alt = teamName;
        wrap.appendChild(img);
      } else {
        const span = document.createElement("span");
        span.className = "flag-fallback";
        span.textContent = teamName ? teamName.slice(0, 2).toUpperCase() : "?";
        wrap.appendChild(span);
      }
      return wrap;
    }

    // ---------- STATE ----------
    const GROUP_LETTERS = Object.keys(OFFICIAL_GROUPS);

    let groupsState = {};
    let thirdPlaced = [];
    let selectedThirds = [];
    let knockoutRounds = [];

    const groupsContainer = document.getElementById("groupsContainer");
    const thirdsListEl = document.getElementById("thirdsList");
    const bracketContainer = document.getElementById("bracketContainer");
    const championNameEl = document.getElementById("championName");
    const championBannerEl = document.getElementById("championBanner");

    const confirmGroupsBtn = document.getElementById("confirmGroupsBtn");
    const resetAllBtn = document.getElementById("resetAllBtn");
    const generateKnockoutBtn = document.getElementById("generateKnockoutBtn");
    const backToGroupsBtn = document.getElementById("backToGroupsBtn");

    const viewGroups = document.getElementById("view-groups");
    const viewKnockout = document.getElementById("view-knockout");

    const userNameInput = document.getElementById("userNameInput");
    const savePredictionBtn = document.getElementById("savePredictionBtn");
    const predictionStatusEl = document.getElementById("predictionStatus");
    const predictionListContainer = document.getElementById("predictionListContainer");

    const PREDICTIONS_KEY = "wc26_predictions_v1";
    let predictions = [];

    function showView(name) {
      if (name === "groups") {
        viewGroups.classList.add("active");
        viewKnockout.classList.remove("active");
      } else {
        viewKnockout.classList.add("active");
        viewGroups.classList.remove("active");
      }
    }

    backToGroupsBtn.addEventListener("click", () => showView("groups"));

    // ---------- GROUPS ----------
    function initGroups() {
      groupsState = {};
      GROUP_LETTERS.forEach(letter => {
        groupsState[letter] = [...OFFICIAL_GROUPS[letter]];
      });
      renderGroups();
    }

    function renderGroups() {
      groupsContainer.innerHTML = "";
      GROUP_LETTERS.forEach(letter => {
        const card = document.createElement("div");
        card.className = "group-card";

        const header = document.createElement("div");
        header.className = "group-header";
        header.innerHTML = `
          <div class="group-name">Group ${letter}</div>
          <div class="group-sub">1st – 4th</div>
        `;
        card.appendChild(header);

        const teams = groupsState[letter];
        teams.forEach((teamName, index) => {
          const row = document.createElement("div");
          row.className = "team-row";

          const left = document.createElement("div");
          left.className = "team-row-left";

          const flag = createFlagElement(teamName);
          const nameSpan = document.createElement("span");
          nameSpan.className = "team-name";
          nameSpan.textContent = teamName;

          left.appendChild(flag);
          left.appendChild(nameSpan);

          const right = document.createElement("div");
          right.style.display = "flex";
          right.style.alignItems = "center";
          right.style.gap = "6px";

          const place = document.createElement("span");
          place.className = "place-pill";
          const posNum = index + 1;
          const posLabel = posNum === 1 ? "1st"
              : posNum === 2 ? "2nd"
              : posNum === 3 ? "3rd" : "4th";
          place.textContent = posLabel;

          const controls = document.createElement("div");
          controls.className = "team-controls";

          const upBtn = document.createElement("button");
          upBtn.className = "icon-btn";
          upBtn.textContent = "▲";
          upBtn.title = "Move up";
          upBtn.disabled = index === 0;

          const downBtn = document.createElement("button");
          downBtn.className = "icon-btn";
          downBtn.textContent = "▼";
          downBtn.title = "Move down";
          downBtn.disabled = index === teams.length - 1;

          upBtn.addEventListener("click", () => moveTeam(letter, index, -1));
          downBtn.addEventListener("click", () => moveTeam(letter, index, +1));

          controls.appendChild(upBtn);
          controls.appendChild(downBtn);

          right.appendChild(place);
          right.appendChild(controls);

          row.appendChild(left);
          row.appendChild(right);
          card.appendChild(row);
        });

        groupsContainer.appendChild(card);
      });
    }

    function moveTeam(groupLetter, index, direction) {
      const arr = groupsState[groupLetter];
      const newIndex = index + direction;
      if (newIndex < 0 || newIndex >= arr.length) return;
      const tmp = arr[index];
      arr[index] = arr[newIndex];
      arr[newIndex] = tmp;
      renderGroups();
    }

    // ---------- THIRD-PLACE ----------
    function confirmGroups() {
      thirdPlaced = GROUP_LETTERS.map(letter => ({
        group: letter,
        name: groupsState[letter][2],
      }));
      selectedThirds = [];
      renderThirdPlacedList();
      alert("Group standings confirmed.\nNow choose exactly 8 third-placed teams on the right.");
    }

    function renderThirdPlacedList() {
      thirdsListEl.innerHTML = "";
      thirdPlaced.forEach(entry => {
        const row = document.createElement("div");
        row.className = "third-item";

        const label = document.createElement("label");
        const cb = document.createElement("input");
        cb.type = "checkbox";

        const flag = createFlagElement(entry.name, true);
        flag.style.width = "24px";
        flag.style.height = "16px";

        const text = document.createElement("span");
        text.textContent = entry.name;

        cb.addEventListener("change", e => onThirdCheckboxChange(e, entry));

        label.appendChild(cb);
        label.appendChild(flag);
        label.appendChild(text);

        const grp = document.createElement("small");
        grp.textContent = `Group ${entry.group} · 3rd`;

        row.appendChild(label);
        row.appendChild(grp);
        thirdsListEl.appendChild(row);
      });

      const info = document.createElement("div");
      info.className = "note";
      info.textContent = "You must select exactly 8 teams.";
      thirdsListEl.appendChild(info);
    }

    function onThirdCheckboxChange(e, entry) {
      if (e.target.checked) {
        if (selectedThirds.length >= 8) {
          e.target.checked = false;
          alert("You can only select 8 third-placed teams.");
          return;
        }
        selectedThirds.push(entry);
      } else {
        selectedThirds = selectedThirds.filter(
          t => !(t.group === entry.group && t.name === entry.name)
        );
      }
    }

    // ---------- KNOCKOUT ----------
    const ROUND_LABELS = [
      "Round of 32",
      "Round of 16",
      "Quarter-finals",
      "Semi-finals",
      "Final",
    ];

    function generateKnockout() {
      if (thirdPlaced.length === 0) {
        alert("Confirm the group standings first.");
        return;
      }
      if (selectedThirds.length !== 8) {
        alert(`You must select exactly 8 third-placed teams.\nCurrently selected: ${selectedThirds.length}`);
        return;
      }

      const winners = [];
      const runnersUp = [];
      GROUP_LETTERS.forEach(letter => {
        winners.push({ name: groupsState[letter][0], tag: `Grp ${letter} 1st` });
        runnersUp.push({ name: groupsState[letter][1], tag: `Grp ${letter} 2nd` });
      });
      const thirds = selectedThirds.map(t => ({
        name: t.name,
        tag: `Grp ${t.group} 3rd`,
      }));

      const qualified = [...winners, ...runnersUp, ...thirds];
      if (qualified.length !== 32) {
        alert("Internal error: expected 32 qualified teams.");
        return;
      }

      const roundOf32 = [];
      for (let i = 0; i < 16; i++) {
        const t1 = qualified[i];
        const t2 = qualified[31 - i];
        roundOf32.push({
          team1: t1,
          team2: t2,
          winnerIndex: null,
          score1: null,
          score2: null,
        });
      }

      const rounds = [roundOf32];
      let prevSize = roundOf32.length;
      while (prevSize > 1) {
        const nextSize = prevSize / 2;
        const round = [];
        for (let i = 0; i < nextSize; i++) {
          round.push({
            team1: null,
            team2: null,
            winnerIndex: null,
            score1: null,
            score2: null,
          });
        }
        rounds.push(round);
        prevSize = nextSize;
      }

      knockoutRounds = rounds;

      championBannerEl.classList.remove("glow");
      championNameEl.textContent =
        "Play through each round to reveal your champion.";
      championNameEl.classList.remove("champion-name");
      championNameEl.classList.add("champion-placeholder");

      propagateWinnersAndRender();
      showView("knockout");
    }

    function winnerObj(match) {
      if (!match || match.winnerIndex === null) return null;
      return match.winnerIndex === 0 ? match.team1 : match.team2;
    }

    function winnerName(match) {
      const obj = winnerObj(match);
      return obj ? obj.name : null;
    }

    function propagateWinnersAndRender() {
      for (let r = 1; r < knockoutRounds.length; r++) {
        const prevRound = knockoutRounds[r - 1];
        const round = knockoutRounds[r];

        for (let m = 0; m < round.length; m++) {
          const match1 = prevRound[m * 2];
          const match2 = prevRound[m * 2 + 1];

          const prev1 = round[m].team1 ? round[m].team1.name : null;
          const prev2 = round[m].team2 ? round[m].team2.name : null;

          round[m].team1 = winnerObj(match1);
          round[m].team2 = winnerObj(match2);

          const new1 = round[m].team1 ? round[m].team1.name : null;
          const new2 = round[m].team2 ? round[m].team2.name : null;

          if (prev1 !== new1 || prev2 !== new2) {
            round[m].winnerIndex = null;
            round[m].score1 = null;
            round[m].score2 = null;
          }
        }
      }

      renderBracket();

      if (knockoutRounds.length > 0) {
        const finalRound = knockoutRounds[knockoutRounds.length - 1];
        const finalMatch = finalRound[0];
        const champ = winnerName(finalMatch);

        if (champ) {
          championBannerEl.classList.add("glow");
          championNameEl.innerHTML = "";
          const flag = createFlagElement(champ, true);
          flag.style.width = "26px";
          flag.style.height = "18px";
          const text = document.createElement("span");
          text.textContent = champ;
          championNameEl.appendChild(flag);
          championNameEl.appendChild(text);
          championNameEl.classList.remove("champion-placeholder");
          championNameEl.classList.add("champion-name");
        } else {
          championBannerEl.classList.remove("glow");
          championNameEl.textContent =
            "Play through each round to reveal your champion.";
          championNameEl.classList.remove("champion-name");
          championNameEl.classList.add("champion-placeholder");
        }
      }
    }

    function renderBracket() {
      bracketContainer.innerHTML = "";

      if (knockoutRounds.length === 0) {
        const msg = document.createElement("div");
        msg.className = "help-text";
        msg.textContent = "Generate the knockout bracket to see all matches.";
        bracketContainer.appendChild(msg);
        return;
      }

      knockoutRounds.forEach((round, roundIndex) => {
        const col = document.createElement("div");
        col.className = "round-column";

        const title = document.createElement("div");
        title.className = "round-title";
        title.textContent = ROUND_LABELS[roundIndex] || `Round ${roundIndex + 1}`;
        col.appendChild(title);

        round.forEach((match, matchIndex) => {
          const matchDiv = document.createElement("div");
          matchDiv.className = "match";

          const t1Line = document.createElement("div");
          t1Line.className = "team-line";

          const t1Btn = document.createElement("button");
          t1Btn.className = "team-btn";
          t1Btn.dataset.round = roundIndex;
          t1Btn.dataset.match = matchIndex;
          t1Btn.dataset.team = 0;

          const t1Inner = document.createElement("span");
          t1Inner.className = "team-btn-inner";

          const t1FlagWrap = createFlagElement(match.team1 ? match.team1.name : "", true);
          const t1Label = document.createElement("span");
          if (match.team1) {
            t1Label.textContent = `${match.team1.name} (${match.team1.tag})`;
            t1Btn.classList.add("filled");
          } else {
            t1Label.textContent = "TBD";
          }
          t1Inner.appendChild(t1FlagWrap);
          t1Inner.appendChild(t1Label);
          t1Btn.appendChild(t1Inner);
          t1Btn.disabled = !match.team1 || !match.team2;
          if (match.winnerIndex === 0) t1Btn.classList.add("winner");

          const score1 = document.createElement("input");
          score1.type = "number";
          score1.min = "0";
          score1.className = "score-input";
          score1.dataset.round = roundIndex;
          score1.dataset.match = matchIndex;
          score1.dataset.team = 0;
          score1.value = match.score1 != null ? match.score1 : "";

          t1Line.appendChild(t1Btn);
          t1Line.appendChild(score1);

          const t2Line = document.createElement("div");
          t2Line.className = "team-line";

          const t2Btn = document.createElement("button");
          t2Btn.className = "team-btn";
          t2Btn.dataset.round = roundIndex;
          t2Btn.dataset.match = matchIndex;
          t2Btn.dataset.team = 1;

          const t2Inner = document.createElement("span");
          t2Inner.className = "team-btn-inner";

          const t2FlagWrap = createFlagElement(match.team2 ? match.team2.name : "", true);
          const t2Label = document.createElement("span");
          if (match.team2) {
            t2Label.textContent = `${match.team2.name} (${match.team2.tag})`;
            t2Btn.classList.add("filled");
          } else {
            t2Label.textContent = "TBD";
          }
          t2Inner.appendChild(t2FlagWrap);
          t2Inner.appendChild(t2Label);
          t2Btn.appendChild(t2Inner);
          t2Btn.disabled = !match.team1 || !match.team2;
          if (match.winnerIndex === 1) t2Btn.classList.add("winner");

          const score2 = document.createElement("input");
          score2.type = "number";
          score2.min = "0";
          score2.className = "score-input";
          score2.dataset.round = roundIndex;
          score2.dataset.match = matchIndex;
          score2.dataset.team = 1;
          score2.value = match.score2 != null ? match.score2 : "";

          t2Line.appendChild(t2Btn);
          t2Line.appendChild(score2);

          matchDiv.appendChild(t1Line);
          matchDiv.appendChild(t2Line);

          const note = document.createElement("div");
          note.className = "match-note";
          note.textContent = "Tip: Use scores. For a draw, click the winner (pens).";
          matchDiv.appendChild(note);

          col.appendChild(matchDiv);
        });

        bracketContainer.appendChild(col);
      });
    }

    // click team = select winner
    bracketContainer.addEventListener("click", e => {
      const btn = e.target.closest(".team-btn");
      if (!btn) return;
      const r = Number(btn.dataset.round);
      const m = Number(btn.dataset.match);
      const t = Number(btn.dataset.team);
      const match = knockoutRounds[r]?.[m];
      if (!match || !match.team1 || !match.team2) return;
      match.winnerIndex = t;
      propagateWinnersAndRender();
    });

    // score inputs
    bracketContainer.addEventListener("input", e => {
      if (!e.target.classList.contains("score-input")) return;
      const r = Number(e.target.dataset.round);
      const m = Number(e.target.dataset.match);
      const t = Number(e.target.dataset.team);
      const match = knockoutRounds[r]?.[m];
      if (!match) return;

      const v = e.target.value === "" ? null : Number(e.target.value);
      if (t === 0) match.score1 = v; else match.score2 = v;

      const s1 = match.score1;
      const s2 = match.score2;

      if (s1 == null || s2 == null || isNaN(s1) || isNaN(s2)) {
        propagateWinnersAndRender();
        return;
      }

      if (s1 > s2) match.winnerIndex = 0;
      else if (s2 > s1) match.winnerIndex = 1;
      else match.winnerIndex = null;

      propagateWinnersAndRender();
    });

    // ---------- PREDICTIONS ----------
    function loadPredictions() {
      const raw = localStorage.getItem(PREDICTIONS_KEY);
      if (!raw) {
        predictions = [];
      } else {
        try {
          predictions = JSON.parse(raw) || [];
        } catch {
          predictions = [];
        }
      }
      renderPredictions();
    }

    function savePredictionsToStorage() {
      localStorage.setItem(PREDICTIONS_KEY, JSON.stringify(predictions));
    }

    function renderPredictions() {
      predictionListContainer.innerHTML = "";
      if (!predictions.length) {
        const empty = document.createElement("div");
        empty.className = "prediction-list-empty";
        empty.textContent = "No predictions yet. Play the knockout and save your champion!";
        predictionListContainer.appendChild(empty);
        return;
      }

      const list = document.createElement("div");
      list.className = "prediction-list";

      predictions.slice().reverse().forEach(p => {
        const card = document.createElement("div");
        card.className = "prediction-card";

        const main = document.createElement("div");
        main.className = "prediction-main";

        const nameEl = document.createElement("div");
        nameEl.className = "prediction-name";
        nameEl.textContent = p.name || "Anonymous";

        const winEl = document.createElement("div");
        winEl.className = "prediction-winner";
        const flag = createFlagElement(p.winner, true);
        flag.style.width = "22px";
        flag.style.height = "16px";
        const span = document.createElement("span");
        span.textContent = "Winner: " + p.winner;
        winEl.appendChild(flag);
        winEl.appendChild(span);

        main.appendChild(nameEl);
        main.appendChild(winEl);

        const meta = document.createElement("div");
        meta.className = "prediction-meta";
        meta.textContent = new Date(p.time).toLocaleString();

        card.appendChild(main);
        card.appendChild(meta);

        list.appendChild(card);
      });

      predictionListContainer.appendChild(list);
    }

    function getCurrentChampionName() {
      if (!knockoutRounds.length) return null;
      const finalRound = knockoutRounds[knockoutRounds.length - 1];
      const finalMatch = finalRound[0];
      return winnerName(finalMatch);
    }

    function handleSavePrediction() {
      const champ = getCurrentChampionName();
      if (!champ) {
        predictionStatusEl.textContent = "You need a champion first – finish the bracket.";
        predictionStatusEl.className = "prediction-status err";
        return;
      }

      const name = userNameInput.value.trim() || "Anonymous";
      const entry = { name, winner: champ, time: new Date().toISOString() };
      predictions.push(entry);
      savePredictionsToStorage();
      renderPredictions();

      predictionStatusEl.textContent = "Saved! Your prediction is added to the list.";
      predictionStatusEl.className = "prediction-status ok";
      userNameInput.value = "";
    }

    savePredictionBtn.addEventListener("click", handleSavePrediction);

    // ---------- RESET ----------
    function resetAll() {
      thirdPlaced = [];
      selectedThirds = [];
      knockoutRounds = [];

      championBannerEl.classList.remove("glow");
      championNameEl.textContent =
        "Generate the bracket and then enter scores / click winners until your champion appears here.";
      championNameEl.classList.remove("champion-name");
      championNameEl.classList.add("champion-placeholder");

      thirdsListEl.innerHTML =
        '<span style="font-size: 0.8rem; color:#6b7280;">Confirm groups first to show all 3rd-place teams.</span>';

      initGroups();
      renderBracket();
      showView("groups");
    }

    // ---------- BIND EVENTS + INIT ----------
    confirmGroupsBtn.addEventListener("click", confirmGroups);
    generateKnockoutBtn.addEventListener("click", generateKnockout);
    resetAllBtn.addEventListener("click", resetAll);

    initGroups();
    renderBracket();   // initial empty state
    loadPredictions();
  </script>
</body>
</html>
