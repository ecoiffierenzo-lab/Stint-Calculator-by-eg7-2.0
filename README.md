# Stint-Calculator-by-eg7-2.0

<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#090b10">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Stint Calculator by EG7</title>
<style>
  :root {
    --bg-dark: #090b10;
    --card-bg: #121620;
    --surface-bg: #191f2d;
    --border-color: #262f42;
    --text-main: #f8fafc;
    --text-muted: #94a3b8;
    --orange: #ff6b00;
    --orange-glow: rgba(255, 107, 0, 0.25);
    --blue: #00a8ff;
    --blue-glow: rgba(0, 168, 255, 0.25);
    --purple: #a855f7;
    --purple-glow: rgba(168, 85, 247, 0.25);
    --success: #10b981;
    --success-bg: rgba(16, 185, 129, 0.12);
    --warning: #f59e0b;
    --warning-bg: rgba(245, 158, 11, 0.15);
    --danger: #ef4444;
    --danger-bg: rgba(239, 68, 68, 0.15);
  }

  /* THÈME MODE NUIT (Vision nocturne muret des stands) */
  body.night-mode {
    --bg-dark: #050202;
    --card-bg: #0e0606;
    --surface-bg: #180a0a;
    --border-color: #361414;
    --text-main: #ff6b6b;
    --text-muted: #a85555;
    --orange: #ff4500;
    --orange-glow: rgba(255, 69, 0, 0.2);
    --blue: #e05252;
    --blue-glow: rgba(224, 82, 82, 0.2);
    --purple: #d946ef;
    --purple-glow: rgba(217, 70, 239, 0.2);
    --success: #d97706;
    --success-bg: rgba(217, 119, 6, 0.12);
    --warning: #f59e0b;
    --warning-bg: rgba(245, 158, 11, 0.14);
    --danger: #ff2a2a;
    --danger-bg: rgba(255, 42, 42, 0.18);
    background-image: none;
  }

  * {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
  }

  html {
    scroll-behavior: smooth;
  }

  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background-color: var(--bg-dark);
    background-image: 
      radial-gradient(circle at 15% 10%, rgba(255, 107, 0, 0.08) 0%, transparent 40%),
      radial-gradient(circle at 85% 90%, rgba(0, 168, 255, 0.08) 0%, transparent 40%);
    color: var(--text-main);
    margin: 0;
    padding: 16px;
    display: flex;
    justify-content: center;
    min-height: 100dvh;
    transition: background-color 0.25s, color 0.25s;
  }

  .app-container {
    width: 100%;
    max-width: 460px;
    padding-bottom: 50vh;
  }

  /* Header & Brand */
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;
    padding: 4px 2px;
    gap: 8px;
  }

  .brand {
    display: flex;
    align-items: center;
    gap: 9px;
    min-width: 0;
  }

  .brand-badge {
    background: linear-gradient(135deg, var(--orange), #d94e00);
    color: #fff;
    font-weight: 900;
    font-style: italic;
    font-size: 1rem;
    padding: 8px 9px;
    border-radius: 12px;
    box-shadow: 0 4px 12px var(--orange-glow);
    letter-spacing: -0.5px;
    flex-shrink: 0;
  }

  .brand-text {
    min-width: 0;
  }

  .brand-text h1 {
    font-size: 0.98rem;
    font-weight: 900;
    font-style: italic;
    margin: 0;
    letter-spacing: 0.2px;
    text-transform: uppercase;
    white-space: nowrap;
  }

  .brand-text p {
    margin: 2px 0 0;
    font-size: 0.74rem;
    color: var(--text-muted);
    font-weight: 500;
  }

  .brand-text span {
    color: var(--orange);
    font-weight: 700;
    font-variant-numeric: tabular-nums;
  }

  .header-actions {
    display: flex;
    align-items: center;
    gap: 5px;
    flex-shrink: 0;
  }

  .btn-header {
    background: var(--surface-bg);
    border: 1px solid var(--border-color);
    color: var(--text-muted);
    font-size: 0.7rem;
    font-weight: 700;
    padding: 7px 8px;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.2s;
    white-space: nowrap;
  }

  .btn-header.active {
    border-color: var(--orange);
    color: var(--text-main);
    background: rgba(255, 107, 0, 0.16);
  }

  .btn-header:active {
    transform: scale(0.95);
  }

  /* Alert Banner */
  #alert-banner {
    border-radius: 14px;
    padding: 13px 14px;
    font-weight: 700;
    font-size: 0.88rem;
    text-align: center;
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    backdrop-filter: blur(8px);
    transition: all 0.25s ease;
  }

  .status-safe {
    background: var(--success-bg);
    color: var(--success);
    border: 1px solid rgba(16, 185, 129, 0.4);
  }

  .status-warning {
    background: var(--warning-bg);
    color: var(--warning);
    border: 1px solid rgba(245, 158, 11, 0.55);
    box-shadow: 0 0 18px rgba(245, 158, 11, 0.15);
  }

  .status-danger {
    background: var(--danger-bg);
    color: var(--danger);
    border: 1px solid rgba(239, 68, 68, 0.6);
    box-shadow: 0 0 20px rgba(239, 68, 68, 0.2);
    animation: alertPulse 2s infinite;
  }

  @keyframes alertPulse {
    0%, 100% { box-shadow: 0 0 12px rgba(239, 68, 68, 0.15); }
    50% { box-shadow: 0 0 24px rgba(239, 68, 68, 0.4); }
  }

  /* FULLSCREEN ALERT OVERLAY */
  #fullscreen-alert {
    position: fixed;
    inset: 0;
    z-index: 9999;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 28px 24px;
    text-align: center;
    backdrop-filter: blur(14px);
    -webkit-backdrop-filter: blur(14px);
    animation: fsPopIn 0.28s cubic-bezier(0.16, 1, 0.3, 1);
  }

  #fullscreen-alert.fs-warning {
    background: radial-gradient(circle at center, rgba(245, 158, 11, 0.32) 0%, rgba(15, 12, 6, 0.96) 75%);
    border: 4px solid var(--warning);
  }

  #fullscreen-alert.fs-danger {
    background: radial-gradient(circle at center, rgba(239, 68, 68, 0.38) 0%, rgba(18, 6, 8, 0.97) 75%);
    border: 4px solid var(--danger);
    animation: fsPopIn 0.28s cubic-bezier(0.16, 1, 0.3, 1), fsBorderFlash 1.2s infinite;
  }

  @keyframes fsPopIn {
    from { opacity: 0; transform: scale(1.06); }
    to { opacity: 1; transform: scale(1); }
  }

  @keyframes fsBorderFlash {
    0%, 100% { box-shadow: inset 0 0 30px rgba(239, 68, 68, 0.35); }
    50% { box-shadow: inset 0 0 70px rgba(239, 68, 68, 0.75); }
  }

  .fs-badge {
    font-size: 0.8rem;
    font-weight: 900;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    padding: 6px 14px;
    border-radius: 99px;
    margin-bottom: 20px;
  }

  .fs-warning .fs-badge {
    background: rgba(245, 158, 11, 0.2);
    color: var(--warning);
    border: 1px solid var(--warning);
  }

  .fs-danger .fs-badge {
    background: rgba(239, 68, 68, 0.25);
    color: #ff6b6b;
    border: 1px solid var(--danger);
  }

  .fs-icon {
    font-size: 4.5rem;
    line-height: 1;
    margin-bottom: 16px;
  }

  .fs-title {
    font-size: 2.1rem;
    font-weight: 900;
    font-style: italic;
    text-transform: uppercase;
    margin: 0 0 12px;
    line-height: 1.1;
    letter-spacing: -0.5px;
  }

  .fs-warning .fs-title { color: var(--warning); }
  .fs-danger .fs-title { color: #ff4d4d; }

  .fs-desc {
    font-size: 1.05rem;
    line-height: 1.5;
    color: var(--text-main);
    max-width: 340px;
    margin: 0 0 24px;
    font-weight: 500;
  }

  .fs-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    width: 100%;
    max-width: 340px;
    margin-bottom: 28px;
  }

  .fs-stat-box {
    background: rgba(255, 255, 255, 0.06);
    border: 1px solid rgba(255, 255, 255, 0.14);
    border-radius: 14px;
    padding: 12px 10px;
  }

  .fs-stat-box span {
    display: block;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-muted);
    margin-bottom: 4px;
    font-weight: 700;
  }

  .fs-stat-box strong {
    font-size: 1.35rem;
    font-weight: 900;
    color: #fff;
    font-variant-numeric: tabular-nums;
  }

  .fs-dismiss-btn {
    width: 100%;
    max-width: 340px;
    padding: 18px;
    border-radius: 16px;
    border: none;
    font-size: 1.05rem;
    font-weight: 900;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    cursor: pointer;
    transition: transform 0.15s;
  }

  .fs-warning .fs-dismiss-btn {
    background: var(--warning);
    color: #090b10;
    box-shadow: 0 8px 25px rgba(245, 158, 11, 0.4);
  }

  .fs-danger .fs-dismiss-btn {
    background: var(--danger);
    color: #fff;
    box-shadow: 0 8px 25px rgba(239, 68, 68, 0.45);
  }

  .fs-dismiss-btn:active {
    transform: scale(0.96);
  }

  /* CUSTOM MODAL DIALOG */
  .modal-backdrop {
    position: fixed;
    inset: 0;
    z-index: 9500;
    background: rgba(5, 7, 12, 0.82);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }

  .modal-card {
    width: 100%;
    max-width: 360px;
    background: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 18px;
    padding: 20px;
    box-shadow: 0 16px 40px rgba(0, 0, 0, 0.6);
  }

  .modal-card h3 {
    margin: 0 0 8px;
    font-size: 1rem;
    font-weight: 900;
    text-transform: uppercase;
    letter-spacing: 0.04em;
    color: var(--text-main);
  }

  .modal-card p {
    margin: 0 0 14px;
    font-size: 0.8rem;
    color: var(--text-muted);
  }

  .modal-card input[type="text"],
  .modal-card input[type="time"] {
    width: 100%;
    background: var(--surface-bg);
    border: 1px solid var(--blue);
    border-radius: 10px;
    padding: 12px;
    color: var(--text-main);
    font-size: 1rem;
    font-weight: 700;
    text-align: center;
    margin-bottom: 14px;
    color-scheme: dark;
  }

  .modal-card input:focus {
    outline: none;
    box-shadow: 0 0 0 3px var(--blue-glow);
  }

  .modal-actions {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
  }

  .btn-modal {
    padding: 11px;
    border-radius: 10px;
    border: none;
    font-size: 0.84rem;
    font-weight: 800;
    cursor: pointer;
    text-transform: uppercase;
  }

  .btn-modal.cancel {
    background: var(--surface-bg);
    color: var(--text-muted);
    border: 1px solid var(--border-color);
  }

  .btn-modal.confirm {
    background: linear-gradient(135deg, var(--orange), #e05600);
    color: #fff;
  }

  /* Section Label Header for Dual Strategy View */
  .strategy-section-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 8px;
    padding: 0 2px;
  }

  .strategy-section-title {
    font-size: 0.72rem;
    font-weight: 900;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--text-muted);
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .strategy-section-sub {
    font-size: 0.7rem;
    font-weight: 700;
    color: var(--text-muted);
  }

  /* Dashboard Metrics */
  .metrics-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 14px;
  }

  .metric-card {
    background: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 14px;
    padding: 13px 10px;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: border-color 0.25s, background 0.25s;
  }

  .metric-card.primary {
    border-color: rgba(255, 107, 0, 0.4);
    background: linear-gradient(180deg, rgba(255, 107, 0, 0.08) 0%, var(--card-bg) 100%);
  }

  .metric-card.primary.joker-low {
    border-color: rgba(245, 158, 11, 0.65);
    background: linear-gradient(180deg, rgba(245, 158, 11, 0.16) 0%, var(--card-bg) 100%);
  }

  .metric-card.primary.joker-zero {
    border-color: rgba(239, 68, 68, 0.7);
    background: linear-gradient(180deg, rgba(239, 68, 68, 0.18) 0%, var(--card-bg) 100%);
  }

  .metric-card.secondary {
    border-color: rgba(0, 168, 255, 0.35);
    background: linear-gradient(180deg, rgba(0, 168, 255, 0.06) 0%, var(--card-bg) 100%);
  }

  .metric-label {
    display: block;
    font-size: 0.68rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-muted);
    margin-bottom: 5px;
  }

  .metric-value {
    font-size: 1.5rem;
    font-weight: 800;
    font-variant-numeric: tabular-nums;
    color: var(--text-main);
  }

  .metric-card.primary .metric-value { color: var(--orange); }
  .metric-card.primary.joker-low .metric-value { color: var(--warning); }
  .metric-card.primary.joker-zero .metric-value { color: var(--danger); }
  .metric-card.secondary .metric-value { color: var(--blue); }

  .metric-sub {
    display: block;
    font-size: 0.68rem;
    color: var(--text-muted);
    margin-top: 4px;
  }

  /* BLOC STRATÉGIQUE TRANCHE HORAIRE / QUOTA INTERMÉDIAIRE */
  .quota-block {
    background: linear-gradient(180deg, rgba(168, 85, 247, 0.09) 0%, var(--card-bg) 100%);
    border: 1px solid rgba(168, 85, 247, 0.45);
    border-radius: 16px;
    padding: 13px;
    margin-bottom: 14px;
    transition: border-color 0.25s, background 0.25s;
  }

  .quota-block.q-validated {
    border-color: rgba(16, 185, 129, 0.55);
    background: linear-gradient(180deg, rgba(16, 185, 129, 0.09) 0%, var(--card-bg) 100%);
  }

  .quota-block.q-warn {
    border-color: rgba(245, 158, 11, 0.7);
    background: linear-gradient(180deg, rgba(245, 158, 11, 0.12) 0%, var(--card-bg) 100%);
  }

  .quota-block.q-danger {
    border-color: rgba(239, 68, 68, 0.8);
    background: linear-gradient(180deg, rgba(239, 68, 68, 0.16) 0%, var(--card-bg) 100%);
  }

  .quota-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    margin-bottom: 8px;
  }

  .quota-title {
    font-size: 0.76rem;
    font-weight: 900;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-main);
  }

  .quota-badge {
    font-size: 0.7rem;
    font-weight: 900;
    padding: 3px 8px;
    border-radius: 7px;
    text-transform: uppercase;
    white-space: nowrap;
  }

  .quota-badge.ok {
    background: var(--success-bg);
    color: var(--success);
    border: 1px solid rgba(16, 185, 129, 0.35);
  }

  .quota-badge.due {
    background: var(--warning-bg);
    color: var(--warning);
    border: 1px solid rgba(245, 158, 11, 0.45);
  }

  .quota-badge.late {
    background: var(--danger-bg);
    color: var(--danger);
    border: 1px solid rgba(239, 68, 68, 0.45);
  }

  .quota-subbar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.76rem;
    font-weight: 700;
    color: var(--text-muted);
    margin-bottom: 10px;
    padding-bottom: 8px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.07);
    font-variant-numeric: tabular-nums;
  }

  .quota-subbar strong {
    color: var(--text-main);
  }

  .quota-metrics-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 8px;
  }

  .q-cell {
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    border-radius: 11px;
    padding: 9px 8px;
    text-align: center;
  }

  .q-cell.q-joker-cell {
    border-color: rgba(168, 85, 247, 0.45);
  }

  .q-cell.q-joker-cell.joker-low {
    border-color: rgba(245, 158, 11, 0.7);
  }

  .q-cell.q-joker-cell.joker-zero {
    border-color: rgba(239, 68, 68, 0.75);
  }

  .q-cell span.q-lbl {
    display: block;
    font-size: 0.64rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted);
    margin-bottom: 3px;
  }

  .q-cell strong.q-val {
    display: block;
    font-size: 1.2rem;
    font-weight: 900;
    color: var(--text-main);
    font-variant-numeric: tabular-nums;
  }

  .q-cell.q-joker-cell strong.q-val { color: var(--purple); }
  .q-cell.q-joker-cell.joker-low strong.q-val { color: var(--warning); }
  .q-cell.q-joker-cell.joker-zero strong.q-val { color: var(--danger); }

  .q-cell span.q-hint {
    display: block;
    font-size: 0.64rem;
    color: var(--text-muted);
    margin-top: 2px;
  }

  /* SIMULATEUR UNDERCUT ("ET SI ON RENTRE MAINTENANT ?") */
  .undercut-card {
    background: linear-gradient(135deg, rgba(0, 168, 255, 0.08) 0%, var(--card-bg) 100%);
    border: 1px solid rgba(0, 168, 255, 0.32);
    border-radius: 14px;
    padding: 12px 14px;
    margin-bottom: 14px;
  }

  .undercut-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 8px;
  }

  .undercut-title {
    font-size: 0.72rem;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--blue);
  }

  .undercut-badge {
    font-size: 0.68rem;
    font-weight: 800;
    padding: 2px 8px;
    border-radius: 6px;
    text-transform: uppercase;
  }

  .undercut-badge.ok {
    background: var(--success-bg);
    color: var(--success);
    border: 1px solid rgba(16, 185, 129, 0.35);
  }

  .undercut-badge.warn {
    background: var(--warning-bg);
    color: var(--warning);
    border: 1px solid rgba(245, 158, 11, 0.45);
  }

  .undercut-badge.risk {
    background: var(--danger-bg);
    color: var(--danger);
    border: 1px solid rgba(239, 68, 68, 0.45);
  }

  .undercut-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
    text-align: center;
  }

  .uc-cell {
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    border-radius: 10px;
    padding: 7px 6px;
  }

  .uc-cell span {
    display: block;
    font-size: 0.64rem;
    font-weight: 700;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 2px;
  }

  .uc-cell strong {
    font-size: 0.96rem;
    font-weight: 900;
    color: var(--text-main);
    font-variant-numeric: tabular-nums;
  }

  /* ACTIVE STINT TRACKER BAR */
  .stint-tracker-card {
    background: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 14px;
    padding: 13px 14px;
    margin-bottom: 14px;
    transition: border-color 0.25s, background 0.25s;
  }

  .stint-tracker-card.stint-warn {
    border-color: rgba(245, 158, 11, 0.7);
    background: linear-gradient(90deg, rgba(245, 158, 11, 0.12) 0%, var(--card-bg) 100%);
  }

  .stint-tracker-card.stint-over {
    border-color: rgba(239, 68, 68, 0.8);
    background: linear-gradient(90deg, rgba(239, 68, 68, 0.16) 0%, var(--card-bg) 100%);
  }

  .stint-top-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 8px;
  }

  .stint-title {
    font-size: 0.72rem;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-muted);
  }

  .stint-box-deadline {
    font-size: 0.76rem;
    font-weight: 800;
    color: var(--orange);
    background: rgba(255, 107, 0, 0.12);
    border: 1px solid rgba(255, 107, 0, 0.35);
    padding: 3px 8px;
    border-radius: 7px;
    font-variant-numeric: tabular-nums;
  }

  .stint-numbers {
    display: flex;
    align-items: baseline;
    justify-content: space-between;
  }

  .stint-elapsed {
    font-size: 1.45rem;
    font-weight: 900;
    font-variant-numeric: tabular-nums;
    color: var(--text-main);
  }

  .stint-remaining-max {
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--text-muted);
    font-variant-numeric: tabular-nums;
  }

  /* Cards & Accordions */
  .card {
    background: var(--card-bg);
    border: 1px solid var(--border-color);
    border-radius: 16px;
    padding: 16px;
    margin-bottom: 14px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.25);
  }

  .card-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    cursor: pointer;
    user-select: none;
  }

  .card-title {
    font-size: 0.84rem;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-main);
    display: flex;
    align-items: center;
    gap: 8px;
    margin: 0;
  }

  .card-title .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--orange);
  }

  .card-title .dot.blue {
    background: var(--blue);
  }

  .card-title .dot.green {
    background: var(--success);
  }

  .toggle-icon {
    color: var(--text-muted);
    font-size: 0.85rem;
    transition: transform 0.25s;
  }

  .card.collapsed .toggle-icon {
    transform: rotate(-90deg);
  }

  .card-body {
    margin-top: 16px;
  }

  .card.collapsed .card-body {
    display: none;
  }

  /* Mode Switcher */
  .mode-tabs {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px;
    background: var(--bg-dark);
    padding: 4px;
    border-radius: 12px;
    border: 1px solid var(--border-color);
    margin-bottom: 14px;
  }

  .mode-tab {
    padding: 9px 8px;
    border-radius: 9px;
    border: none;
    background: transparent;
    color: var(--text-muted);
    font-size: 0.78rem;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
  }

  .mode-tab.active {
    background: var(--surface-bg);
    color: var(--text-main);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  /* Preset Chips */
  .preset-chips {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 6px;
    margin-top: 8px;
  }

  .chip-btn {
    background: var(--surface-bg);
    border: 1px solid var(--border-color);
    color: var(--text-muted);
    border-radius: 9px;
    padding: 8px 2px;
    font-size: 0.76rem;
    font-weight: 800;
    cursor: pointer;
    transition: all 0.15s;
  }

  .chip-btn.active {
    background: rgba(0, 168, 255, 0.16);
    border-color: var(--blue);
    color: #fff;
  }

  .chip-btn:active {
    transform: scale(0.94);
  }

  /* Calculated End Time Preview Banner */
  .end-preview-box {
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    padding: 12px 14px;
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .end-preview-label {
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.04em;
  }

  .end-preview-value {
    font-size: 1.05rem;
    font-weight: 900;
    color: var(--blue);
    font-variant-numeric: tabular-nums;
  }

  .btn-now-inline {
    background: rgba(255, 107, 0, 0.15);
    border: 1px solid rgba(255, 107, 0, 0.45);
    color: var(--orange);
    border-radius: 8px;
    padding: 4px 8px;
    font-size: 0.7rem;
    font-weight: 800;
    cursor: pointer;
  }

  .btn-now-inline:active {
    transform: scale(0.95);
  }

  /* Live Clock Box */
  .live-clock-display {
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    border-radius: 14px;
    padding: 15px 14px;
    text-align: center;
    margin-bottom: 12px;
  }

  .live-clock-display.red-flag-paused {
    border-color: var(--danger);
    background: rgba(239, 68, 68, 0.08);
  }

  .live-clock-status {
    font-size: 0.72rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--blue);
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }

  .pulse-dot {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: var(--success);
    animation: pulse 1.5s infinite;
  }

  @keyframes pulse {
    0% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.8); }
    100% { opacity: 1; transform: scale(1); }
  }

  .live-countdown {
    font-size: 2.1rem;
    font-weight: 900;
    font-variant-numeric: tabular-nums;
    letter-spacing: 1px;
    color: var(--text-main);
  }

  .live-subinfo {
    font-size: 0.74rem;
    color: var(--text-muted);
    margin-top: 4px;
  }

  .session-btn-row {
    display: grid;
    grid-template-columns: 1.3fr 1fr;
    gap: 8px;
  }

  .btn-session {
    width: 100%;
    padding: 13px 10px;
    border-radius: 12px;
    border: none;
    font-size: 0.84rem;
    font-weight: 900;
    cursor: pointer;
    transition: all 0.2s;
    text-transform: uppercase;
    letter-spacing: 0.03em;
  }

  .btn-session.start {
    background: linear-gradient(135deg, var(--blue), #0077cc);
    color: #fff;
    box-shadow: 0 4px 14px var(--blue-glow);
  }

  .btn-session.redflag {
    background: rgba(239, 68, 68, 0.18);
    color: #ff6b6b;
    border: 1px solid rgba(239, 68, 68, 0.55);
  }

  .btn-session.resume {
    background: linear-gradient(135deg, var(--success), #059669);
    color: #fff;
  }

  .btn-session.stop {
    background: var(--surface-bg);
    color: var(--text-muted);
    border: 1px solid var(--border-color);
  }

  .btn-session:active {
    transform: scale(0.97);
  }

  /* Pit Log History (Interactive editable tags) */
  .pit-log-box {
    margin-top: 12px;
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    border-radius: 11px;
    padding: 10px 12px;
  }

  .pit-log-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.7rem;
    font-weight: 800;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 8px;
  }

  .pit-log-list {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .pit-tag {
    background: var(--surface-bg);
    border: 1px solid var(--border-color);
    border-radius: 8px;
    padding: 6px 9px;
    font-size: 0.74rem;
    font-weight: 700;
    color: var(--text-main);
    font-variant-numeric: tabular-nums;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    gap: 5px;
    transition: border-color 0.15s, transform 0.1s;
  }

  .pit-tag:active {
    transform: scale(0.94);
    border-color: var(--blue);
  }

  .pit-tag span.num {
    color: var(--orange);
    font-weight: 900;
  }

  .pit-tag span.edit-ico {
    color: var(--blue);
    font-size: 0.7rem;
  }

  /* Rule Presets Bottom Card */
  .rule-presets-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .preset-slot {
    background: var(--surface-bg);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    padding: 10px 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
  }

  .preset-slot-info {
    min-width: 0;
    flex: 1;
  }

  .preset-slot-title {
    font-size: 0.84rem;
    font-weight: 800;
    color: var(--text-main);
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .preset-slot-sub {
    font-size: 0.7rem;
    color: var(--text-muted);
    margin-top: 2px;
  }

  .preset-slot-actions {
    display: flex;
    gap: 6px;
    flex-shrink: 0;
  }

  .btn-mini {
    background: var(--bg-dark);
    border: 1px solid var(--border-color);
    color: var(--text-muted);
    border-radius: 8px;
    padding: 7px 10px;
    font-size: 0.72rem;
    font-weight: 800;
    cursor: pointer;
    text-transform: uppercase;
  }

  .btn-mini.load {
    color: var(--blue);
    border-color: rgba(0, 168, 255, 0.4);
  }

  .btn-mini.save {
    color: var(--orange);
    border-color: rgba(255, 107, 0, 0.4);
  }

  .btn-mini:active {
    transform: scale(0.94);
  }

  /* Inputs & Steppers */
  .input-group {
    margin-bottom: 14px;
  }

  .input-group:last-child {
    margin-bottom: 0;
  }

  .row-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  label {
    display: block;
    font-size: 0.74rem;
    font-weight: 600;
    color: var(--text-muted);
    margin-bottom: 6px;
    line-height: 1.25;
  }

  .label-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 6px;
  }

  .label-row label {
    margin-bottom: 0;
  }

  input[type="number"],
  input[type="time"] {
    width: 100%;
    background: var(--surface-bg);
    border: 1px solid var(--border-color);
    border-radius: 10px;
    padding: 11px 10px;
    color: var(--text-main);
    font-size: 1.02rem;
    font-weight: 700;
    font-variant-numeric: tabular-nums;
    text-align: center;
    scroll-margin-top: 80px;
    scroll-margin-bottom: 240px;
    transition: border-color 0.2s, box-shadow 0.2s;
    color-scheme: dark;
  }

  input[type="number"]:focus,
  input[type="time"]:focus {
    outline: none;
    border-color: var(--blue);
    box-shadow: 0 0 0 3px var(--blue-glow);
  }

  /* Time Inputs */
  .time-inputs {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 8px;
  }

  .time-inputs-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px;
  }

  .time-box span {
    display: block;
    font-size: 0.68rem;
    font-weight: 700;
    color: var(--text-muted);
    text-align: center;
    margin-top: 4px;
    text-transform: uppercase;
  }

  /* Pit Counter with +/- Buttons */
  .pit-stepper {
    display: grid;
    grid-template-columns: 52px 1fr 52px;
    gap: 8px;
    align-items: center;
  }

  .btn-step {
    height: 44px;
    border-radius: 10px;
    border: 1px solid var(--border-color);
    background: var(--surface-bg);
    color: var(--text-main);
    font-size: 1.3rem;
    font-weight: 700;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.15s;
  }

  .btn-step.plus {
    background: linear-gradient(135deg, var(--orange), #e05600);
    border: none;
    color: #fff;
    box-shadow: 0 4px 12px var(--orange-glow);
  }

  .btn-step:active {
    transform: scale(0.93);
  }

  /* Quick Action Copy Button */
  .btn-copy {
    width: 100%;
    padding: 13px;
    border-radius: 12px;
    border: 1px solid var(--border-color);
    background: var(--surface-bg);
    color: var(--text-main);
    font-size: 0.85rem;
    font-weight: 700;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-bottom: 14px;
    transition: all 0.2s;
  }

  .btn-copy:active {
    background: var(--border-color);
    transform: scale(0.98);
  }

  /* Progress Bar */
  .progress-wrap {
    margin-top: 12px;
    background: var(--surface-bg);
    height: 6px;
    border-radius: 99px;
    overflow: hidden;
  }

  .progress-bar {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, var(--orange), var(--blue));
    transition: width 0.3s ease;
  }

  .hidden {
    display: none !important;
  }
</style>
</head>
<body>

<!-- ALERTE PLEIN ÉCRAN (1 JOKER / 0 JOKER) -->
<div id="fullscreen-alert" class="hidden" role="alertdialog" aria-modal="true">
  <div class="fs-badge" id="fsBadge">ALERTE STRATÉGIE EG7</div>
  <div class="fs-icon" id="fsIcon">⚠️</div>
  <h2 class="fs-title" id="fsTitle">PLUS QUE 1 JOKER</h2>
  <p class="fs-desc" id="fsDesc">Attention, il ne reste qu'un seul arrêt joker de marge avant d'être bloqué sur les temps minimums.</p>
  <div class="fs-stats">
    <div class="fs-stat-box">
      <span>Stint Min. Immédiat</span>
      <strong id="fsMinNext">0m 00s</strong>
    </div>
    <div class="fs-stat-box">
      <span>Stint Moyen Requis</span>
      <strong id="fsMinAvg">0m 00s</strong>
    </div>
  </div>
  <button type="button" class="fs-dismiss-btn" onclick="dismissFullscreenAlert()">J'AI COMPRIS</button>
</div>

<!-- MODALE NOM DU PRESET -->
<div id="presetNameModal" class="modal-backdrop hidden" role="dialog" aria-modal="true">
  <div class="modal-card">
    <h3>Nommer le préréglage</h3>
    <p>Donne un nom à cette configuration de règlement pour la retrouver facilement.</p>
    <input type="text" id="presetNameInput" maxlength="28" placeholder="Ex: 24H Brignoles, 6H SWS...">
    <div class="modal-actions">
      <button type="button" class="btn-modal cancel" onclick="closePresetModal()">Annuler</button>
      <button type="button" class="btn-modal confirm" onclick="confirmSavePreset()">Enregistrer</button>
    </div>
  </div>
</div>

<!-- MODALE MODIFICATION HEURE D'UN PIT -->
<div id="editPitModal" class="modal-backdrop hidden" role="dialog" aria-modal="true">
  <div class="modal-card">
    <h3 id="editPitTitle">Modifier l'arrêt #1</h3>
    <p>Choisis l'heure exacte à laquelle ce passage aux stands a été effectué.</p>
    <input type="time" id="editPitTimeInput">
    <div class="modal-actions">
      <button type="button" class="btn-modal cancel" onclick="closeEditPitModal()">Annuler</button>
      <button type="button" class="btn-modal confirm" onclick="confirmEditPitTime()">Valider l'heure</button>
    </div>
  </div>
</div>

<div class="app-container">
  <header>
    <div class="brand">
      <div class="brand-badge">EG7</div>
      <div class="brand-text">
        <h1>Stint Calculator</h1>
        <p><span id="headerClock">--:--:--</span></p>
      </div>
    </div>
    <div class="header-actions">
      <button type="button" class="btn-header" id="nightModeBtn" onclick="toggleNightMode()">🌙 Nuit</button>
      <button type="button" class="btn-header" onclick="resetAll()">Reset</button>
    </div>
  </header>

  <!-- Bannière de statut -->
  <div id="alert-banner"></div>

  <!-- 1. VUE STRATÉGIE COURSE GLOBALE -->
  <div class="strategy-section-bar">
    <span class="strategy-section-title">🏁 Course Globale</span>
    <span class="strategy-section-sub" id="globalSectionSub">Objectif total</span>
  </div>
  <div class="metrics-grid">
    <div class="metric-card primary" id="jokerCard">
      <span class="metric-label">Jokers Globaux</span>
      <span class="metric-value" id="jokers">0</span>
      <span class="metric-sub" id="pitsLeftText">0 arrêt restant</span>
    </div>
    <div class="metric-card secondary">
      <span class="metric-label">Marge Globale</span>
      <span class="metric-value" id="margin">0m 00s</span>
      <span class="metric-sub">Avant dépassement max</span>
    </div>
    <div class="metric-card">
      <span class="metric-label">Stint Min. Immédiat</span>
      <span class="metric-value" id="minNext">0m 00s</span>
      <span class="metric-sub">Ce relais minimum</span>
    </div>
    <div class="metric-card">
      <span class="metric-label">Stint Moyen Requis</span>
      <span class="metric-value" id="minAvg">0m 00s</span>
      <span class="metric-sub">Avant fermeture pits</span>
    </div>
  </div>

  <!-- 2. VUE STRATÉGIE TRANCHE HORAIRE / QUOTA INTERMÉDIAIRE -->
  <div class="quota-block hidden" id="quotaBlock">
    <div class="quota-header">
      <span class="quota-title" id="qBlockTitle">🎯 Tranche : 3 arrêts avant 3h</span>
      <span class="quota-badge ok" id="qBlockBadge">0 / 3 FAITS</span>
    </div>
    <div class="quota-subbar">
      <span id="qDeadlineText">Échéance : 3h de course</span>
      <strong id="qTimeLeftText">Reste 3h 00m</strong>
    </div>
    <div class="quota-metrics-grid">
      <div class="q-cell q-joker-cell" id="qJokerCell">
        <span class="q-lbl">Jokers Tranche</span>
        <strong class="q-val" id="qJokersVal">0</strong>
        <span class="q-hint" id="qPitsLeftHint">0 arrêt restant</span>
      </div>
      <div class="q-cell">
        <span class="q-lbl">Marge Tranche</span>
        <strong class="q-val" id="qMarginVal">0m 00s</strong>
        <span class="q-hint">Avant fin tranche</span>
      </div>
      <div class="q-cell">
        <span class="q-lbl">Stint Min. Tranche</span>
        <strong class="q-val" id="qMinNextVal">0m 00s</strong>
        <span class="q-hint">Relais min. immédiat</span>
      </div>
      <div class="q-cell">
        <span class="q-lbl">Moy. Requis Tranche</span>
        <strong class="q-val" id="qMinAvgVal">0m 00s</strong>
        <span class="q-hint">Cadence avant limite</span>
      </div>
    </div>
  </div>

  <!-- SIMULATEUR UNDERCUT ("ET SI ON RENTRE MAINTENANT ?") -->
  <div class="undercut-card hidden" id="undercutCard">
    <div class="undercut-header">
      <span class="undercut-title">⚡ Et si on rentre maintenant ?</span>
      <span class="undercut-badge ok" id="ucBadge">Faisable</span>
    </div>
    <div class="undercut-grid">
      <div class="uc-cell">
        <span>Jokers après</span>
        <strong id="ucJokersAfter">0</strong>
      </div>
      <div class="uc-cell">
        <span>Moy. restante</span>
        <strong id="ucAvgAfter">0m 00s</strong>
      </div>
      <div class="uc-cell">
        <span>Relais actuel</span>
        <strong id="ucCurrentStint">0m 00s</strong>
      </div>
    </div>
  </div>

  <!-- SUIVI DU RELAIS EN COURS & HEURE LIMITE BOX -->
  <div class="stint-tracker-card hidden" id="stintTrackerCard">
    <div class="stint-top-row">
      <span class="stint-title" id="currentStintLabel">⏱️ Relais #1 en cours</span>
      <span class="stint-box-deadline" id="boxBeforeLabel">BOX avant --:--</span>
    </div>
    <div class="stint-numbers">
      <span class="stint-elapsed" id="stintElapsedDisplay">00:00</span>
      <span class="stint-remaining-max" id="stintMaxLeftDisplay">Max dans --m</span>
    </div>
  </div>

  <!-- Suivi Live -->
  <div class="card">
    <div class="card-header" onclick="toggleCard(this)">
      <h2 class="card-title"><span class="dot blue"></span> Suivi Live Course</h2>
      <span class="toggle-icon">▼</span>
    </div>
    <div class="card-body">

      <!-- Sélecteur Mode Auto (Horloge téléphone) / Manuel -->
      <div class="mode-tabs">
        <button type="button" class="mode-tab active" id="tabAuto" onclick="setMode('auto')">🕒 Session Horloge</button>
        <button type="button" class="mode-tab" id="tabManual" onclick="setMode('manual')">⌨️ Chrono Manuel</button>
      </div>

      <!-- MODE AUTO : Heure de départ + Durée de la course -->
      <div id="panelAuto">
        <div id="sessionSetup">
          <div class="input-group row-2">
            <div>
              <div class="label-row">
                <label for="startTime">Heure départ</label>
                <button type="button" class="btn-now-inline" onclick="setStartNow()">Maintenant</button>
              </div>
              <input type="time" id="startTime" onchange="onScheduleChange()">
            </div>
            <div>
              <label for="durationQuick">Durée (h)</label>
              <input type="number" id="durationQuick" value="0" step="0.5" min="0" inputmode="decimal" onfocus="handleFocus(this)" oninput="syncDurationFromQuick(this.value)">
            </div>
          </div>

          <!-- Raccourcis rapides de durée -->
          <div class="input-group">
            <div class="preset-chips">
              <button type="button" class="chip-btn" onclick="selectQuickDuration(1)">1h</button>
              <button type="button" class="chip-btn" onclick="selectQuickDuration(2)">2h</button>
              <button type="button" class="chip-btn" onclick="selectQuickDuration(4)">4h</button>
              <button type="button" class="chip-btn" onclick="selectQuickDuration(6)">6h</button>
              <button type="button" class="chip-btn" onclick="selectQuickDuration(12)">12h</button>
              <button type="button" class="chip-btn" onclick="selectQuickDuration(24)">24h</button>
            </div>
          </div>

          <!-- Aperçu de la fin calculée automatiquement -->
          <div class="end-preview-box">
            <span class="end-preview-label">🏁 Fin calculée</span>
            <span class="end-preview-value" id="calculatedEndPreview">--:--</span>
          </div>

          <button type="button" class="btn-session start" onclick="startSession()">▶ Lancer la session live</button>
        </div>

        <div id="sessionRunning" class="hidden">
          <div class="live-clock-display" id="liveClockBox">
            <div class="live-clock-status" id="sessionStatusLabel">
              <span class="pulse-dot"></span> Synchronisé sur l'heure du téléphone
            </div>
            <div class="live-countdown" id="liveCountdown">00:00:00</div>
            <div class="live-subinfo" id="liveScheduleSummary"></div>
          </div>
          <div class="session-btn-row">
            <button type="button" class="btn-session redflag" id="redFlagBtn" onclick="toggleRedFlag()">🚩 Drapeau Rouge</button>
            <button type="button" class="btn-session stop" onclick="stopSession()">⏹ Modifier</button>
          </div>
        </div>
      </div>

      <!-- MODE MANUEL -->
      <div id="panelManual" class="hidden">
        <div class="input-group">
          <label>Temps restant au chrono</label>
          <div class="time-inputs">
            <div class="time-box">
              <input type="number" id="remH" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
              <span>Heures</span>
            </div>
            <div class="time-box">
              <input type="number" id="remM" value="0" min="0" max="59" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
              <span>Minutes</span>
            </div>
            <div class="time-box">
              <input type="number" id="remS" value="0" min="0" max="59" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
              <span>Secondes</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Compteur d'arrêts (commun aux 2 modes) -->
      <div class="input-group" style="margin-top: 16px;">
        <label for="donePits">Arrêts déjà effectués</label>
        <div class="pit-stepper">
          <button type="button" class="btn-step" onclick="stepPits(-1)">−</button>
          <input type="number" id="donePits" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="onDonePitsManualInput()">
          <button type="button" class="btn-step plus" onclick="stepPits(1)">+</button>
        </div>
        <div class="progress-wrap">
          <div class="progress-bar" id="pitProgress"></div>
        </div>

        <!-- Historique horodaté des arrêts (cliquable pour modifier l'heure) -->
        <div class="pit-log-box hidden" id="pitLogBox">
          <div class="pit-log-header">
            <span>📋 Journal des passages (touche pour modifier)</span>
            <span id="pitLogCount">0 arrêt</span>
          </div>
          <div class="pit-log-list" id="pitLogList"></div>
        </div>
      </div>

    </div>
  </div>

  <!-- Paramètres Règlement -->
  <div class="card" id="rulesCard">
    <div class="card-header" onclick="toggleCard(this)">
      <h2 class="card-title"><span class="dot"></span> Paramètres Règlement</h2>
      <span class="toggle-icon">▼</span>
    </div>
    <div class="card-body">

      <div class="input-group row-2">
        <div>
          <label for="totalHours">Durée course (h)</label>
          <input type="number" id="totalHours" value="0" step="0.5" min="0" inputmode="decimal" onfocus="handleFocus(this)" oninput="syncDurationFromRules(this.value)">
        </div>
        <div>
          <label for="reqPits">Arrêts obligatoires</label>
          <input type="number" id="reqPits" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
      </div>

      <div class="input-group row-2">
        <div>
          <label for="minStint">Stint min (min)</label>
          <input type="number" id="minStint" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
        <div>
          <label for="maxStint">Stint max (min)</label>
          <input type="number" id="maxStint" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
      </div>

      <div class="input-group row-2">
        <div>
          <label for="pitOpen">Ouverture stands après départ (min)</label>
          <input type="number" id="pitOpen" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
        <div>
          <label for="pitClose">Fermeture stands avant arrivée (min)</label>
          <input type="number" id="pitClose" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
      </div>

      <div class="input-group">
        <label>Durée immobilisation pit</label>
        <div class="time-inputs-2">
          <div class="time-box">
            <input type="number" id="pitMin" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
            <span>Minutes</span>
          </div>
          <div class="time-box">
            <input type="number" id="pitSec" value="0" min="0" max="59" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
            <span>Secondes</span>
          </div>
        </div>
      </div>

      <!-- Quota intermédiaire : X arrêts dans les X premières heures -->
      <div class="input-group row-2">
        <div>
          <label for="quotaPits">Tranche : Arrêts min. requis (0 = aucun)</label>
          <input type="number" id="quotaPits" value="0" min="0" inputmode="numeric" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
        <div>
          <label for="quotaHours">Dans les X premières heures</label>
          <input type="number" id="quotaHours" value="0" step="0.5" min="0" inputmode="decimal" onfocus="handleFocus(this)" oninput="calculate()">
        </div>
      </div>

    </div>
  </div>

  <!-- Bouton partage rapide WhatsApp / équipe -->
  <button class="btn-copy" onclick="copySummary()" id="copyBtn">
    📋 Copier le point stratégie pour l'équipe
  </button>

  <!-- Préréglages de règlements tout en bas -->
  <div class="card" id="presetsCard">
    <div class="card-header" onclick="toggleCard(this)">
      <h2 class="card-title"><span class="dot green"></span> Préréglages Règlements</h2>
      <span class="toggle-icon">▼</span>
    </div>
    <div class="card-body">
      <div class="rule-presets-grid">
        <div class="preset-slot">
          <div class="preset-slot-info">
            <div class="preset-slot-title" id="presetName0">Emplacement 1 (vide)</div>
            <div class="preset-slot-sub" id="presetSub0">Aucun paramètre enregistré</div>
          </div>
          <div class="preset-slot-actions">
            <button type="button" class="btn-mini load" onclick="loadRulePreset(0)">Charger</button>
            <button type="button" class="btn-mini save" onclick="openSavePresetModal(0)">Sauver</button>
          </div>
        </div>

        <div class="preset-slot">
          <div class="preset-slot-info">
            <div class="preset-slot-title" id="presetName1">Emplacement 2 (vide)</div>
            <div class="preset-slot-sub" id="presetSub1">Aucun paramètre enregistré</div>
          </div>
          <div class="preset-slot-actions">
            <button type="button" class="btn-mini load" onclick="loadRulePreset(1)">Charger</button>
            <button type="button" class="btn-mini save" onclick="openSavePresetModal(1)">Sauver</button>
          </div>
        </div>

        <div class="preset-slot">
          <div class="preset-slot-info">
            <div class="preset-slot-title" id="presetName2">Emplacement 3 (vide)</div>
            <div class="preset-slot-sub" id="presetSub2">Aucun paramètre enregistré</div>
          </div>
          <div class="preset-slot-actions">
            <button type="button" class="btn-mini load" onclick="loadRulePreset(2)">Charger</button>
            <button type="button" class="btn-mini save" onclick="openSavePresetModal(2)">Sauver</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
const NUM_FIELDS = [
  'totalHours', 'reqPits', 'minStint', 'maxStint',
  'pitOpen', 'pitMin', 'pitSec', 'pitClose',
  'quotaPits', 'quotaHours', 'remH', 'remM', 'remS', 'donePits'
];

const RULE_FIELDS = [
  'totalHours', 'reqPits', 'minStint', 'maxStint',
  'pitOpen', 'pitMin', 'pitSec', 'pitClose',
  'quotaPits', 'quotaHours'
];

let currentMode = 'auto';
let sessionActive = false;
let sessionStartMs = null;
let sessionEndMs = null;

// Drapeau rouge (gel du chrono)
let isRedFlag = false;
let redFlagStartedAtMs = null;
let pausedRemainingMs = 0;

// Suivi des relais et journal des arrêts
let pitLogs = [];
let editingPitIndex = null;
let savingPresetSlot = null;

let lastJokerCount = null;
let acknowledgedLevel = null;
let nightMode = false;
let wakeLockSentinel = null;

async function requestWakeLock() {
  if ('wakeLock' in navigator && !wakeLockSentinel) {
    try {
      wakeLockSentinel = await navigator.wakeLock.request('screen');
      wakeLockSentinel.addEventListener('release', () => {
        wakeLockSentinel = null;
      });
    } catch (e) {}
  }
}

function releaseWakeLock() {
  if (wakeLockSentinel) {
    wakeLockSentinel.release().catch(() => {});
    wakeLockSentinel = null;
  }
}

document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'visible' && sessionActive) {
    requestWakeLock();
  }
});

function toggleNightMode() {
  nightMode = !nightMode;
  document.body.classList.toggle('night-mode', nightMode);
  document.getElementById('nightModeBtn').classList.toggle('active', nightMode);
  saveState();
}

function handleFocus(inputEl) {
  inputEl.select();
  setTimeout(() => {
    inputEl.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }, 300);
}

function setMode(mode) {
  currentMode = mode;
  document.getElementById('tabAuto').classList.toggle('active', mode === 'auto');
  document.getElementById('tabManual').classList.toggle('active', mode === 'manual');
  document.getElementById('panelAuto').classList.toggle('hidden', mode !== 'auto');
  document.getElementById('panelManual').classList.toggle('hidden', mode !== 'manual');
  saveState();
  calculate();
}

function setStartNow() {
  const now = new Date();
  const hh = String(now.getHours()).padStart(2, '0');
  const mm = String(now.getMinutes()).padStart(2, '0');
  document.getElementById('startTime').value = `${hh}:${mm}`;
  onScheduleChange();
}

function selectQuickDuration(hours) {
  document.getElementById('durationQuick').value = hours;
  document.getElementById('totalHours').value = hours;
  highlightDurationChip(hours);
  onScheduleChange();
}

function syncDurationFromQuick(val) {
  document.getElementById('totalHours').value = val;
  highlightDurationChip(parseFloat(val || 0));
  onScheduleChange();
}

function syncDurationFromRules(val) {
  document.getElementById('durationQuick').value = val;
  highlightDurationChip(parseFloat(val || 0));
  onScheduleChange();
}

function highlightDurationChip(hours) {
  document.querySelectorAll('.chip-btn').forEach(btn => {
    const val = parseFloat(btn.innerText);
    btn.classList.toggle('active', val === hours);
  });
}

function computeScheduleBounds() {
  const timeVal = document.getElementById('startTime').value;
  const durHours = parseFloat(document.getElementById('totalHours').value || 0);

  if (!timeVal || durHours <= 0) return null;

  const [hh, mm] = timeVal.split(':').map(Number);
  const now = new Date();
  let start = new Date(now.getFullYear(), now.getMonth(), now.getDate(), hh, mm, 0, 0);
  let end = new Date(start.getTime() + durHours * 3600 * 1000);

  if (end.getTime() < now.getTime() && (start.getTime() + 86400000 - now.getTime()) < 12 * 3600 * 1000) {
    start = new Date(start.getTime() + 86400000);
    end = new Date(start.getTime() + durHours * 3600 * 1000);
  }

  return { start, end, durHours };
}

function onScheduleChange() {
  const bounds = computeScheduleBounds();
  const previewEl = document.getElementById('calculatedEndPreview');

  if (!bounds) {
    previewEl.innerText = '--:--';
  } else {
    const { start, end } = bounds;
    const endTimeStr = end.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
    const crossesMidnight = end.getDate() !== start.getDate() || end.getMonth() !== start.getMonth();
    previewEl.innerText = crossesMidnight ? `${endTimeStr} (+1 jour)` : endTimeStr;
  }

  saveState();
  calculate();
}

function updateRunningSummaryText() {
  if (!sessionStartMs || !sessionEndMs) return;
  const sObj = new Date(sessionStartMs);
  const eObj = new Date(sessionEndMs);
  const sStr = sObj.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
  const eStr = eObj.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
  const nextDay = eObj.getDate() !== sObj.getDate() ? ' (+1j)' : '';
  document.getElementById('liveScheduleSummary').innerText = `Départ : ${sStr} → Fin calculée : ${eStr}${nextDay}`;
}

function startSession() {
  const bounds = computeScheduleBounds();
  if (!bounds) {
    alert('Renseigne l\'heure de départ et la durée de la course avant de lancer.');
    return;
  }

  sessionStartMs = bounds.start.getTime();
  sessionEndMs = bounds.end.getTime();
  sessionActive = true;
  isRedFlag = false;
  redFlagStartedAtMs = null;
  pausedRemainingMs = 0;

  document.getElementById('sessionSetup').classList.add('hidden');
  document.getElementById('sessionRunning').classList.remove('hidden');
  updateRedFlagUI();
  updateRunningSummaryText();
  requestWakeLock();
  recalculatePitDurations();

  saveState();
  calculate();
}

function stopSession() {
  sessionActive = false;
  sessionStartMs = null;
  sessionEndMs = null;
  isRedFlag = false;
  redFlagStartedAtMs = null;
  pausedRemainingMs = 0;

  document.getElementById('sessionSetup').classList.remove('hidden');
  document.getElementById('sessionRunning').classList.add('hidden');
  releaseWakeLock();

  saveState();
  calculate();
}

function toggleRedFlag() {
  if (!sessionActive) return;
  const nowMs = Date.now();

  if (!isRedFlag) {
    isRedFlag = true;
    redFlagStartedAtMs = nowMs;
    pausedRemainingMs = Math.max(0, sessionEndMs - nowMs);
  } else {
    const pauseDurationMs = nowMs - redFlagStartedAtMs;
    sessionEndMs += pauseDurationMs;
    isRedFlag = false;
    redFlagStartedAtMs = null;
    updateRunningSummaryText();
  }

  updateRedFlagUI();
  saveState();
  calculate();
}

function updateRedFlagUI() {
  const btn = document.getElementById('redFlagBtn');
  const box = document.getElementById('liveClockBox');
  if (isRedFlag) {
    btn.className = 'btn-session resume';
    btn.innerText = '▶ Relancer course';
    box.classList.add('red-flag-paused');
  } else {
    btn.className = 'btn-session redflag';
    btn.innerText = '🚩 Drapeau Rouge';
    box.classList.remove('red-flag-paused');
  }
}

/* PRÉRÉGLAGES DE RÈGLEMENTS */
function getSavedPresets() {
  try {
    return JSON.parse(localStorage.getItem('eg7_rule_presets_v2') || '[null, null, null]');
  } catch (e) {
    return [null, null, null];
  }
}

function renderPresetNames() {
  const presets = getSavedPresets();
  for (let i = 0; i < 3; i++) {
    const titleEl = document.getElementById(`presetName${i}`);
    const subEl = document.getElementById(`presetSub${i}`);
    if (presets[i]) {
      titleEl.innerText = presets[i].name || `Préréglage ${i + 1}`;
      subEl.innerText = `${presets[i].totalHours}h • ${presets[i].reqPits} pits • Min ${presets[i].minStint}m / Max ${presets[i].maxStint}m`;
    } else {
      titleEl.innerText = `Emplacement ${i + 1} (vide)`;
      subEl.innerText = 'Aucun paramètre enregistré';
    }
  }
}

function openSavePresetModal(slotIdx) {
  savingPresetSlot = slotIdx;
  const presets = getSavedPresets();
  const h = document.getElementById('totalHours').value || '0';
  const p = document.getElementById('reqPits').value || '0';
  const defaultName = presets[slotIdx]?.name || `Course ${h}H (${p} pits)`;

  const input = document.getElementById('presetNameInput');
  input.value = defaultName;
  document.getElementById('presetNameModal').classList.remove('hidden');
  setTimeout(() => {
    input.focus();
    input.select();
  }, 80);
}

function closePresetModal() {
  savingPresetSlot = null;
  document.getElementById('presetNameModal').classList.add('hidden');
}

function confirmSavePreset() {
  if (savingPresetSlot === null) return;
  const rawName = document.getElementById('presetNameInput').value.trim();
  const h = document.getElementById('totalHours').value || '0';
  const finalName = rawName || `Course ${h}H`;

  const presets = getSavedPresets();
  const data = { name: finalName };
  RULE_FIELDS.forEach(id => {
    data[id] = document.getElementById(id).value;
  });
  presets[savingPresetSlot] = data;
  localStorage.setItem('eg7_rule_presets_v2', JSON.stringify(presets));

  renderPresetNames();
  closePresetModal();
}

function loadRulePreset(slotIdx) {
  const presets = getSavedPresets();
  const data = presets[slotIdx];
  if (!data) {
    alert(`Aucun règlement enregistré dans l'emplacement ${slotIdx + 1}. Clique sur "Sauver" pour enregistrer les paramètres actuels.`);
    return;
  }
  RULE_FIELDS.forEach(id => {
    if (data[id] !== undefined) {
      document.getElementById(id).value = data[id];
    }
  });
  document.getElementById('durationQuick').value = data.totalHours || '0';
  highlightDurationChip(parseFloat(data.totalHours || 0));
  onScheduleChange();
}

/* COMPTEUR D'ARRÊTS, JOURNAL HORODATÉ & ÉDITION DES HEURES */
function recalculatePitDurations() {
  pitLogs.sort((a, b) => a.timestamp - b.timestamp);

  for (let i = 0; i < pitLogs.length; i++) {
    pitLogs[i].num = i + 1;
    const prevTs = i === 0
      ? (sessionStartMs || pitLogs[i].timestamp)
      : pitLogs[i - 1].timestamp;
    pitLogs[i].stintDurMin = Math.max(0, Math.round((pitLogs[i].timestamp - prevTs) / 60000));
  }
  renderPitLogs();
}

function stepPits(delta) {
  const input = document.getElementById('donePits');
  const current = parseInt(input.value || 0, 10);
  const next = Math.max(0, current + delta);
  input.value = next;

  const now = new Date();
  const nowMs = now.getTime();

  if (delta > 0) {
    const timeStr = now.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
    pitLogs.push({
      num: next,
      timeStr,
      timestamp: nowMs,
      stintDurMin: 0
    });
    recalculatePitDurations();
  } else if (delta < 0 && pitLogs.length > 0) {
    pitLogs.pop();
    recalculatePitDurations();
  }

  calculate();
}

function onDonePitsManualInput() {
  const target = Math.max(0, parseInt(document.getElementById('donePits').value || 0, 10));
  const now = new Date();
  const nowMs = now.getTime();
  const timeStr = now.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });

  while (pitLogs.length < target) {
    pitLogs.push({
      num: pitLogs.length + 1,
      timeStr,
      timestamp: nowMs,
      stintDurMin: 0
    });
  }
  while (pitLogs.length > target) {
    pitLogs.pop();
  }
  recalculatePitDurations();
  calculate();
}

function openEditPitModal(index) {
  const item = pitLogs[index];
  if (!item) return;
  editingPitIndex = index;

  document.getElementById('editPitTitle').innerText = `Modifier l'arrêt #${item.num}`;
  const dt = new Date(item.timestamp);
  const hh = String(dt.getHours()).padStart(2, '0');
  const mm = String(dt.getMinutes()).padStart(2, '0');
  document.getElementById('editPitTimeInput').value = `${hh}:${mm}`;

  document.getElementById('editPitModal').classList.remove('hidden');
}

function closeEditPitModal() {
  editingPitIndex = null;
  document.getElementById('editPitModal').classList.add('hidden');
}

function confirmEditPitTime() {
  if (editingPitIndex === null || !pitLogs[editingPitIndex]) return;
  const timeVal = document.getElementById('editPitTimeInput').value;
  if (!timeVal) return;

  const [hh, mm] = timeVal.split(':').map(Number);
  const baseDate = new Date(sessionStartMs || pitLogs[editingPitIndex].timestamp || Date.now());
  let updatedDate = new Date(baseDate.getFullYear(), baseDate.getMonth(), baseDate.getDate(), hh, mm, 0, 0);

  if (sessionStartMs && updatedDate.getTime() < sessionStartMs - 15 * 60000) {
    updatedDate = new Date(updatedDate.getTime() + 86400000);
  }

  pitLogs[editingPitIndex].timestamp = updatedDate.getTime();
  pitLogs[editingPitIndex].timeStr = updatedDate.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });

  recalculatePitDurations();
  closeEditPitModal();
  calculate();
}

function renderPitLogs() {
  const box = document.getElementById('pitLogBox');
  const list = document.getElementById('pitLogList');
  const countEl = document.getElementById('pitLogCount');

  if (pitLogs.length === 0) {
    box.classList.add('hidden');
    return;
  }

  box.classList.remove('hidden');
  countEl.innerText = `${pitLogs.length} arrêt${pitLogs.length > 1 ? 's' : ''}`;
  list.innerHTML = pitLogs.map((p, idx) =>
    `<button type="button" class="pit-tag" onclick="openEditPitModal(${idx})">
      <span class="num">#${p.num}</span> ${p.timeStr} (${p.stintDurMin}m) <span class="edit-ico">✎</span>
    </button>`
  ).join('');
}

/* SIMULATEUR UNDERCUT ("ET SI ON RENTRE MAINTENANT ?") */
function updateUndercutSimulator(P_rem, T_rem, S_min, S_max, P_dur, T_close) {
  const card = document.getElementById('undercutCard');
  if (P_rem <= 0 || T_rem <= 0 || S_max <= 0) {
    card.classList.add('hidden');
    return;
  }

  card.classList.remove('hidden');

  const P_rem_after = P_rem - 1;
  const T_rem_after = Math.max(0, T_rem - P_dur);
  const N_stints_after = P_rem_after + 1;
  const T_track_after = Math.max(0, T_rem_after - (P_rem_after * P_dur));
  const T_cap_after = N_stints_after * S_max;

  const nowMs = isRedFlag && redFlagStartedAtMs ? redFlagStartedAtMs : Date.now();
  let curStintMin = 0;
  if (sessionActive && sessionStartMs && nowMs >= sessionStartMs) {
    const stintStartMs = pitLogs.length > 0 ? pitLogs[pitLogs.length - 1].timestamp : sessionStartMs;
    curStintMin = Math.max(0, (nowMs - stintStartMs) / 60000);
  }
  document.getElementById('ucCurrentStint').innerText = sessionActive ? formatMinutes(curStintMin) : '--';

  let jokersAfter = 0;
  if (P_rem_after > 0) {
    const minPitsNeeded = Math.max(1, Math.ceil((T_rem_after - S_max) / (S_max + P_dur)));
    jokersAfter = Math.max(0, P_rem_after - minPitsNeeded);
  }

  const avgAfter = N_stints_after > 0 ? (T_track_after / N_stints_after) : 0;

  document.getElementById('ucJokersAfter').innerText = T_cap_after < T_track_after ? 'IMPOSSIBLE' : jokersAfter;
  document.getElementById('ucAvgAfter').innerText = formatMinutes(avgAfter);

  const badge = document.getElementById('ucBadge');
  badge.classList.remove('ok', 'warn', 'risk');

  if (T_cap_after < T_track_after || (P_rem_after > 0 && T_rem_after <= T_close)) {
    badge.classList.add('risk');
    badge.innerText = 'Trop tôt (dépasse max)';
  } else if (sessionActive && S_min > 0 && curStintMin < S_min) {
    badge.classList.add('risk');
    badge.innerText = `Sous stint min (${S_min}m)`;
  } else if (jokersAfter === 0) {
    badge.classList.add('warn');
    badge.innerText = '0 joker restant';
  } else {
    badge.classList.add('ok');
    badge.innerText = `OK (${jokersAfter} joker${jokersAfter > 1 ? 's' : ''})`;
  }
}

/* BLOC STRATÉGIQUE TRANCHE HORAIRE : X ARRÊTS DANS LES X PREMIÈRES HEURES */
function updateIntermediateQuota(T_total, T_rem, P_done, S_min, S_max, P_dur) {
  const block = document.getElementById('quotaBlock');
  const qPits = parseInt(document.getElementById('quotaPits').value || 0, 10);
  const qHours = parseFloat(document.getElementById('quotaHours').value || 0);

  if (qPits <= 0 || qHours <= 0 || T_total <= 0) {
    block.classList.add('hidden');
    return;
  }

  block.classList.remove('hidden', 'q-validated', 'q-warn', 'q-danger');

  const qLimitMin = Math.min(T_total, qHours * 60);
  const elapsedMin = Math.max(0, T_total - T_rem);
  const qRemMin = Math.max(0, qLimitMin - elapsedMin);
  const qPitsRem = Math.max(0, qPits - P_done);

  document.getElementById('qBlockTitle').innerText = `🎯 Tranche : ${qPits} arrêt${qPits > 1 ? 's' : ''} avant ${qHours}h`;
  document.getElementById('qPitsLeftHint').innerText = `${qPitsRem} arrêt${qPitsRem > 1 ? 's' : ''} restant${qPitsRem > 1 ? 's' : ''}`;

  let deadlineLabel = `Limite : ${qHours}h de course`;
  const bounds = sessionActive && sessionStartMs
    ? { start: new Date(sessionStartMs) }
    : computeScheduleBounds();

  if (bounds && bounds.start) {
    const deadlineDate = new Date(bounds.start.getTime() + qLimitMin * 60000);
    const timeStr = deadlineDate.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
    deadlineLabel = `Avant ${timeStr} (${qHours}h)`;
  }
  document.getElementById('qDeadlineText').innerText = deadlineLabel;

  const hLeft = Math.floor(qRemMin / 60);
  const mLeft = Math.ceil(qRemMin % 60);
  const timeLeftStr = qRemMin <= 0 ? 'Échéance atteinte' : (hLeft > 0 ? `Reste ${hLeft}h ${String(mLeft).padStart(2, '0')}m` : `Reste ${mLeft} min`);
  document.getElementById('qTimeLeftText').innerText = timeLeftStr;

  const badge = document.getElementById('qBlockBadge');
  const jokerCell = document.getElementById('qJokerCell');
  badge.classList.remove('ok', 'due', 'late');
  jokerCell.classList.remove('joker-low', 'joker-zero');

  if (qPitsRem === 0) {
    block.classList.add('q-validated');
    badge.classList.add('ok');
    badge.innerText = `VALIDÉ (${P_done}/${qPits}) ✓`;
    document.getElementById('qJokersVal').innerText = 'OK';
    document.getElementById('qMarginVal').innerText = formatMinutes(qRemMin);
    document.getElementById('qMinNextVal').innerText = 'Libre';
    document.getElementById('qMinAvgVal').innerText = 'Validé';
    return;
  }

  badge.innerText = `${P_done} / ${qPits} FAIT${P_done > 1 ? 'S' : ''}`;

  if (qRemMin <= 0) {
    block.classList.add('q-danger');
    badge.classList.add('late');
    jokerCell.classList.add('joker-zero');
    document.getElementById('qJokersVal').innerText = '0';
    document.getElementById('qMarginVal').innerText = 'DÉPASSÉ';
    document.getElementById('qMinNextVal').innerText = 'BOX NOW';
    document.getElementById('qMinAvgVal').innerText = 'BOX NOW';
    return;
  }

  const N_q_stints = qPitsRem + 1;
  const T_q_track_rem = Math.max(0, qRemMin - (qPitsRem * P_dur));
  const T_q_cap_max = S_max > 0 ? N_q_stints * S_max : 0;

  let qJokers = 0;
  if (S_max > 0 && qPitsRem > 0) {
    const minPitsNeededQ = Math.max(1, Math.ceil((qRemMin - S_max) / (S_max + P_dur)));
    qJokers = Math.max(0, qPitsRem - minPitsNeededQ);
  }

  const qMargin = S_max > 0 ? (T_q_cap_max - T_q_track_rem) : 0;
  const qMinNextCalc = S_max > 0 ? Math.max(0, T_q_track_rem - (qPitsRem * S_max)) : 0;
  const qMinNext = Math.max(S_min, qMinNextCalc);
  const qMinAvg = qPitsRem > 0 ? Math.max(S_min, T_q_track_rem / qPitsRem) : T_q_track_rem;

  document.getElementById('qJokersVal').innerText = S_max > 0 ? qJokers : '-';
  document.getElementById('qMarginVal').innerText = S_max > 0 ? (qMargin >= 0 ? formatMinutes(qMargin) : `-${formatMinutes(Math.abs(qMargin))}`) : '-';
  document.getElementById('qMinNextVal').innerText = S_max > 0 ? formatMinutes(qMinNext) : '-';
  document.getElementById('qMinAvgVal').innerText = S_max > 0 ? formatMinutes(qMinAvg) : '-';

  const minTimeNeededForQuota = qPitsRem * (S_min + P_dur);
  if ((S_max > 0 && qMargin < 0) || (S_min > 0 && minTimeNeededForQuota > qRemMin)) {
    block.classList.add('q-danger');
    badge.classList.add('late');
    jokerCell.classList.add('joker-zero');
  } else if (S_max > 0 && qJokers === 0) {
    block.classList.add('q-danger');
    badge.classList.add('late');
    jokerCell.classList.add('joker-zero');
  } else if (S_max > 0 && qJokers === 1) {
    block.classList.add('q-warn');
    badge.classList.add('due');
    jokerCell.classList.add('joker-low');
  } else {
    badge.classList.add('ok');
  }
}

/* SUIVI DU RELAIS EN COURS & HEURE LIMITE BOX */
function updateStintTracker(S_max, T_rem_min, P_rem) {
  const card = document.getElementById('stintTrackerCard');
  if (!sessionActive || !sessionStartMs || S_max <= 0) {
    card.classList.add('hidden');
    return;
  }

  const nowMs = isRedFlag && redFlagStartedAtMs ? redFlagStartedAtMs : Date.now();
  if (nowMs < sessionStartMs || T_rem_min <= 0) {
    card.classList.add('hidden');
    return;
  }

  card.classList.remove('hidden', 'stint-warn', 'stint-over');

  const stintStartMs = pitLogs.length > 0
    ? pitLogs[pitLogs.length - 1].timestamp
    : sessionStartMs;

  const elapsedSec = Math.max(0, Math.floor((nowMs - stintStartMs) / 1000));
  const elapsedMin = elapsedSec / 60;
  const maxRemMin = S_max - elapsedMin;

  const stintNum = pitLogs.length + 1;
  document.getElementById('currentStintLabel').innerText = `⏱️ Relais #${stintNum} en cours`;

  const m = Math.floor(elapsedSec / 60);
  const s = elapsedSec % 60;
  document.getElementById('stintElapsedDisplay').innerText = `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;

  const hardMaxMs = Math.min(stintStartMs + S_max * 60000, sessionEndMs);
  const deadlineStr = new Date(hardMaxMs).toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
  document.getElementById('boxBeforeLabel').innerText = P_rem > 0 ? `BOX avant ${deadlineStr}` : `Fin à ${deadlineStr}`;

  if (maxRemMin <= 0) {
    card.classList.add('stint-over');
    document.getElementById('stintMaxLeftDisplay').innerText = `⚠️ STINT MAX DÉPASSÉ (+${Math.abs(Math.floor(maxRemMin))}m)`;
  } else if (maxRemMin <= 3 && P_rem > 0) {
    card.classList.add('stint-warn');
    document.getElementById('stintMaxLeftDisplay').innerText = `🟠 BOX DANS ${Math.ceil(maxRemMin)} MIN MAX`;
  } else {
    document.getElementById('stintMaxLeftDisplay').innerText = `Max (${S_max}m) dans ${Math.ceil(maxRemMin)}m`;
  }
}

function saveState() {
  const state = {
    currentMode,
    sessionActive,
    sessionStartMs,
    sessionEndMs,
    isRedFlag,
    redFlagStartedAtMs,
    pausedRemainingMs,
    pitLogs,
    nightMode,
    startTime: document.getElementById('startTime').value,
    durationQuick: document.getElementById('durationQuick').value
  };
  NUM_FIELDS.forEach(id => {
    state[id] = document.getElementById(id).value;
  });
  localStorage.setItem('eg7_stint_calc_v10', JSON.stringify(state));
}

function loadState() {
  renderPresetNames();
  const saved = localStorage.getItem('eg7_stint_calc_v10');
  if (saved) {
    try {
      const state = JSON.parse(saved);
      NUM_FIELDS.forEach(id => {
        if (state[id] !== undefined) {
          document.getElementById(id).value = state[id];
        }
      });
      if (state.nightMode) {
        nightMode = true;
        document.body.classList.add('night-mode');
        document.getElementById('nightModeBtn').classList.add('active');
      }
      if (Array.isArray(state.pitLogs)) {
        pitLogs = state.pitLogs;
        renderPitLogs();
      }
      if (state.startTime) document.getElementById('startTime').value = state.startTime;
      if (state.durationQuick !== undefined) {
        document.getElementById('durationQuick').value = state.durationQuick;
      } else {
        document.getElementById('durationQuick').value = document.getElementById('totalHours').value;
      }
      highlightDurationChip(parseFloat(document.getElementById('totalHours').value || 0));
      onScheduleChange();

      if (state.currentMode) setMode(state.currentMode);
      if (state.sessionActive && state.sessionStartMs && state.sessionEndMs) {
        sessionStartMs = state.sessionStartMs;
        sessionEndMs = state.sessionEndMs;
        sessionActive = true;
        isRedFlag = !!state.isRedFlag;
        redFlagStartedAtMs = state.redFlagStartedAtMs || null;
        pausedRemainingMs = state.pausedRemainingMs || 0;

        document.getElementById('sessionSetup').classList.add('hidden');
        document.getElementById('sessionRunning').classList.remove('hidden');
        updateRedFlagUI();
        updateRunningSummaryText();
        requestWakeLock();
      }
    } catch (e) {}
  }
}

function resetAll() {
  NUM_FIELDS.forEach(id => {
    document.getElementById(id).value = '0';
  });
  document.getElementById('startTime').value = '';
  document.getElementById('durationQuick').value = '0';
  document.getElementById('calculatedEndPreview').innerText = '--:--';
  sessionActive = false;
  sessionStartMs = null;
  sessionEndMs = null;
  isRedFlag = false;
  redFlagStartedAtMs = null;
  pausedRemainingMs = 0;
  pitLogs = [];
  lastJokerCount = null;
  acknowledgedLevel = null;

  renderPitLogs();
  highlightDurationChip(0);
  releaseWakeLock();
  document.getElementById('undercutCard').classList.add('hidden');
  document.getElementById('quotaBlock').classList.add('hidden');
  document.getElementById('stintTrackerCard').classList.add('hidden');
  document.getElementById('fullscreen-alert').classList.add('hidden');
  document.getElementById('sessionSetup').classList.remove('hidden');
  document.getElementById('sessionRunning').classList.add('hidden');
  localStorage.removeItem('eg7_stint_calc_v10');
  calculate();
}

function toggleCard(headerEl) {
  headerEl.parentElement.classList.toggle('collapsed');
}

function formatMinutes(totalMins) {
  if (totalMins <= 0) return '0m 00s';
  const mins = Math.floor(totalMins);
  const secs = Math.round((totalMins - mins) * 60);
  if (secs === 60) {
    return `${mins + 1}m 00s`;
  }
  return `${mins}m ${secs.toString().padStart(2, '0')}s`;
}

function formatHMS(totalSeconds) {
  const sec = Math.max(0, Math.floor(totalSeconds));
  const h = Math.floor(sec / 3600);
  const m = Math.floor((sec % 3600) / 60);
  const s = sec % 60;
  return `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
}

function getRemainingMinutes() {
  const T_total = parseFloat(document.getElementById('totalHours').value || 0) * 60;

  if (currentMode === 'auto') {
    if (sessionActive && isRedFlag) {
      const remSec = pausedRemainingMs / 1000;
      document.getElementById('sessionStatusLabel').innerHTML = `🚩 DRAPEAU ROUGE — CHRONO GELÉ`;
      document.getElementById('liveCountdown').innerText = formatHMS(remSec);
      return remSec / 60;
    }

    let startMs = sessionStartMs;
    let endMs = sessionEndMs;

    if (!sessionActive || !startMs || !endMs) {
      const bounds = computeScheduleBounds();
      if (!bounds) return T_total;
      startMs = bounds.start.getTime();
      endMs = bounds.end.getTime();
    }

    const nowMs = Date.now();
    const statusLabel = document.getElementById('sessionStatusLabel');
    const countdownEl = document.getElementById('liveCountdown');

    if (nowMs < startMs) {
      const totalCourseSec = Math.max(0, (endMs - startMs) / 1000);
      const waitSec = (startMs - nowMs) / 1000;
      if (statusLabel) statusLabel.innerHTML = `<span class="pulse-dot" style="background:var(--warning)"></span> Départ dans ${formatHMS(waitSec)}`;
      if (countdownEl) countdownEl.innerText = formatHMS(totalCourseSec);
      return totalCourseSec / 60;
    } else if (nowMs >= endMs) {
      if (statusLabel) statusLabel.innerHTML = `🏁 Course terminée`;
      if (countdownEl) countdownEl.innerText = '00:00:00';
      return 0;
    } else {
      const remSec = (endMs - nowMs) / 1000;
      if (statusLabel) statusLabel.innerHTML = `<span class="pulse-dot"></span> En cours • Horloge téléphone`;
      if (countdownEl) countdownEl.innerText = formatHMS(remSec);
      return remSec / 60;
    }
  } else {
    const h = parseFloat(document.getElementById('remH').value || 0);
    const m = parseFloat(document.getElementById('remM').value || 0);
    const s = parseFloat(document.getElementById('remS').value || 0);
    const T_rem_input = (h * 60) + m + (s / 60);
    return T_total > 0 ? Math.min(T_total, Math.max(0, T_rem_input)) : Math.max(0, T_rem_input);
  }
}

function showFullscreenAlert(level, minNextStr, minAvgStr) {
  const fsEl = document.getElementById('fullscreen-alert');
  const fsIcon = document.getElementById('fsIcon');
  const fsTitle = document.getElementById('fsTitle');
  const fsDesc = document.getElementById('fsDesc');

  fsEl.classList.remove('fs-warning', 'fs-danger', 'hidden');
  document.getElementById('fsMinNext').innerText = minNextStr;
  document.getElementById('fsMinAvg').innerText = minAvgStr;

  if (level === 'one') {
    fsEl.classList.add('fs-warning');
    fsIcon.innerText = '⚠️';
    fsTitle.innerText = 'PLUS QUE 1 JOKER !';
    fsDesc.innerText = 'Il ne te reste qu’un seul arrêt joker de sécurité. Surveille tes temps de relais avant d’être bloqué.';
    if (navigator.vibrate) navigator.vibrate([250, 100, 250]);
  } else if (level === 'zero') {
    fsEl.classList.add('fs-danger');
    fsIcon.innerText = '🚨';
    fsTitle.innerText = '0 JOKER RESTANT !';
    fsDesc.innerText = 'Plus aucune marge disponible ! Chaque relais restant doit impérativement respecter le temps minimum.';
    if (navigator.vibrate) navigator.vibrate([500, 120, 500, 120, 500]);
  }
}

function dismissFullscreenAlert() {
  document.getElementById('fullscreen-alert').classList.add('hidden');
}

function handleJokerAlerts(jokers, P_rem, T_rem, minNextStr, minAvgStr) {
  const jokerCard = document.getElementById('jokerCard');
  jokerCard.classList.remove('joker-low', 'joker-zero');

  if (P_rem <= 0 || T_rem <= 0) {
    acknowledgedLevel = null;
    lastJokerCount = jokers;
    return;
  }

  if (jokers === 0) {
    jokerCard.classList.add('joker-zero');
    if (acknowledgedLevel !== 'zero' && (lastJokerCount === null || lastJokerCount >= 1)) {
      acknowledgedLevel = 'zero';
      showFullscreenAlert('zero', minNextStr, minAvgStr);
    }
  } else if (jokers === 1) {
    jokerCard.classList.add('joker-low');
    if (acknowledgedLevel !== 'one' && (lastJokerCount === null || lastJokerCount > 1)) {
      acknowledgedLevel = 'one';
      showFullscreenAlert('one', minNextStr, minAvgStr);
    }
  } else {
    acknowledgedLevel = null;
    dismissFullscreenAlert();
  }

  lastJokerCount = jokers;
}

function calculate() {
  saveState();

  const T_total = parseFloat(document.getElementById('totalHours').value || 0) * 60;
  const P_req = parseInt(document.getElementById('reqPits').value || 0);
  const S_min = parseFloat(document.getElementById('minStint').value || 0);
  const S_max = parseFloat(document.getElementById('maxStint').value || 0);
  const T_open_start = parseFloat(document.getElementById('pitOpen').value || 0);

  const pitM = parseFloat(document.getElementById('pitMin').value || 0);
  const pitS = parseFloat(document.getElementById('pitSec').value || 0);
  const P_dur = pitM + (pitS / 60);

  const T_close = parseFloat(document.getElementById('pitClose').value || 0);
  const T_rem = getRemainingMinutes();
  const P_done = parseInt(document.getElementById('donePits').value || 0);

  const P_rem = Math.max(0, P_req - P_done);
  document.getElementById('pitsLeftText').innerText = `${P_rem} arrêt${P_rem > 1 ? 's' : ''} restant${P_rem > 1 ? 's' : ''}`;
  document.getElementById('globalSectionSub').innerText = `${P_done}/${P_req} arrêts`;

  const progress = P_req > 0 ? Math.min(100, (P_done / P_req) * 100) : 0;
  document.getElementById('pitProgress').style.width = `${progress}%`;

  updateStintTracker(S_max, T_rem, P_rem);
  updateIntermediateQuota(T_total, T_rem, P_done, S_min, S_max, P_dur);
  updateUndercutSimulator(P_rem, T_rem, S_min, S_max, P_dur, T_close);

  const alertBanner = document.getElementById('alert-banner');
  const jokerCard = document.getElementById('jokerCard');

  if (S_max <= 0) {
    jokerCard.classList.remove('joker-low', 'joker-zero');
    alertBanner.className = 'status-warning';
    alertBanner.innerHTML = `<span>⏱️</span> Renseigne les paramètres du règlement pour démarrer`;
    document.getElementById('jokers').innerText = '0';
    document.getElementById('margin').innerText = '0m 00s';
    document.getElementById('minNext').innerText = '0m 00s';
    document.getElementById('minAvg').innerText = '0m 00s';
    return;
  }

  const N_rem_stints = P_rem + 1;
  const T_track_rem = Math.max(0, T_rem - (P_rem * P_dur));
  const T_cap_max = N_rem_stints * S_max;
  const T_open = Math.max(0, T_rem - T_close);

  if (P_rem > 0 && T_rem <= T_close) {
    jokerCard.classList.remove('joker-low');
    jokerCard.classList.add('joker-zero');
    alertBanner.className = 'status-danger';
    alertBanner.innerHTML = `<span>🚫</span> STANDS FERMÉS : Il manque ${P_rem} arrêt(s) !`;
    document.getElementById('jokers').innerText = '0';
    document.getElementById('margin').innerText = '0m 00s';
    document.getElementById('minNext').innerText = '0m 00s';
    document.getElementById('minAvg').innerText = '0m 00s';
    return;
  }

  if (P_rem > 0 && T_close > S_max) {
    jokerCard.classList.remove('joker-low');
    jokerCard.classList.add('joker-zero');
    const excessLastStint = T_close - S_max;
    alertBanner.className = 'status-danger';
    alertBanner.innerHTML = `<span>⚠️</span> IMPOSSIBLE : Fermeture (${T_close}m) > Stint max (${S_max}m)`;
    document.getElementById('jokers').innerText = '0';
    document.getElementById('margin').innerText = `-${formatMinutes(excessLastStint)}`;
    document.getElementById('minNext').innerText = formatMinutes(S_max);
    document.getElementById('minAvg').innerText = formatMinutes(S_max);
    return;
  }

  if (T_cap_max < T_track_rem) {
    jokerCard.classList.remove('joker-low');
    jokerCard.classList.add('joker-zero');
    const deficit = T_rem - (T_cap_max + P_rem * P_dur);
    const extraPits = Math.ceil(deficit / (S_max + P_dur));
    alertBanner.className = 'status-danger';
    alertBanner.innerHTML = `<span>⚠️</span> ALERTE : +${extraPits} arrêt(s) obligatoire(s) en plus !`;
    
    document.getElementById('jokers').innerText = '0';
    document.getElementById('margin').innerText = `-${formatMinutes(deficit)}`;
    document.getElementById('minNext').innerText = formatMinutes(S_max);
    document.getElementById('minAvg').innerText = formatMinutes(S_max);
    return;
  }

  const minTimeForRemainingStints = (P_rem * (S_min + P_dur)) + (P_rem > 0 ? Math.max(S_min, T_close) : S_min);
  if (S_min > 0 && minTimeForRemainingStints > T_rem) {
    jokerCard.classList.remove('joker-low');
    jokerCard.classList.add('joker-zero');
    const excessTime = minTimeForRemainingStints - T_rem;
    alertBanner.className = 'status-danger';
    alertBanner.innerHTML = `<span>⚠️</span> IMPOSSIBLE : Trop d'arrêts (${formatMinutes(excessTime)} de trop)`;
    
    document.getElementById('jokers').innerText = '0';
    document.getElementById('margin').innerText = formatMinutes(T_cap_max - T_track_rem);
    document.getElementById('minNext').innerText = formatMinutes(S_min);
    document.getElementById('minAvg').innerText = formatMinutes(Math.max(0, (T_open - P_rem * P_dur)) / Math.max(1, P_rem));
    return;
  }

  let jokers = 0;
  if (P_rem > 0) {
    const minPitsNeeded = Math.max(1, Math.ceil((T_rem - S_max) / (S_max + P_dur)));
    jokers = Math.max(0, P_rem - minPitsNeeded);
  }

  const margin = T_cap_max - T_track_rem;
  const minNext_calc = Math.max(0, T_track_rem - (P_rem * S_max));
  const minNext = Math.max(S_min, minNext_calc);

  const T_track_before_close = Math.max(0, T_open - (P_rem * P_dur));
  const minAvg = P_rem > 0 ? Math.max(S_min, T_track_before_close / P_rem) : T_track_rem;

  const minNextStr = formatMinutes(minNext);
  const minAvgStr = formatMinutes(minAvg);

  handleJokerAlerts(jokers, P_rem, T_rem, minNextStr, minAvgStr);

  const elapsedCourseMin = T_total > 0 ? Math.max(0, T_total - T_rem) : 9999;
  const standsLockedStart = T_open_start > 0 && elapsedCourseMin < T_open_start && P_rem > 0;

  if (P_rem === 0) {
    alertBanner.className = 'status-safe';
    alertBanner.innerHTML = `<span>🏁</span> DERNIER RELAIS : Tous les arrêts sont faits !`;
  } else if (standsLockedStart) {
    const openIn = Math.ceil(T_open_start - elapsedCourseMin);
    alertBanner.className = 'status-warning';
    alertBanner.innerHTML = `<span>🔒</span> STANDS FERMÉS (Départ) : Ouverture dans ${openIn} min`;
  } else if (jokers === 0) {
    alertBanner.className = 'status-danger';
    alertBanner.innerHTML = `<span>🚨</span> ALERTE 0 JOKER : Plus aucune marge ! Respecte les temps min.`;
  } else if (jokers === 1) {
    alertBanner.className = 'status-warning';
    alertBanner.innerHTML = `<span>⚠️</span> ATTENTION : Il ne reste plus que 1 seul joker !`;
  } else {
    alertBanner.className = 'status-safe';
    alertBanner.innerHTML = `<span>🟢</span> STRATÉGIE OK : ${jokers} jokers disponibles`;
  }

  document.getElementById('jokers').innerText = jokers;
  document.getElementById('margin').innerText = formatMinutes(margin);
  document.getElementById('minNext').innerText = minNextStr;
  document.getElementById('minAvg').innerText = minAvgStr;
}

function copySummary() {
  const T_rem_sec = getRemainingMinutes() * 60;
  const remStr = formatHMS(T_rem_sec);
  const done = document.getElementById('donePits').value;
  const req = document.getElementById('reqPits').value;
  const jokers = document.getElementById('jokers').innerText;
  const minNext = document.getElementById('minNext').innerText;
  const minAvg = document.getElementById('minAvg').innerText;
  const boxDeadline = document.getElementById('boxBeforeLabel').innerText;

  const qPits = parseInt(document.getElementById('quotaPits').value || 0, 10);
  const qHours = parseFloat(document.getElementById('quotaHours').value || 0);
  let quotaLine = '';
  if (qPits > 0 && qHours > 0) {
    const qJokers = document.getElementById('qJokersVal').innerText;
    const qAvg = document.getElementById('qMinAvgVal').innerText;
    quotaLine = `\n• Tranche (${qPits} pits / ${qHours}h) : *${qJokers} joker(s)* • Moy. ${qAvg}`;
  }

  const stintLine = sessionActive ? `\n• Relais en cours : *${boxDeadline}*` : '';
  const text = `🏁 *Point Stratégie EG7* (${remStr} restants)\n• Pits : ${done}/${req}\n• Jokers globaux : *${jokers}*\n• Stint min immédiat : *${minNext}*\n• Stint moyen requis : *${minAvg}*${quotaLine}${stintLine}`;
  
  navigator.clipboard.writeText(text).then(() => {
    const btn = document.getElementById('copyBtn');
    const oldText = btn.innerHTML;
    btn.innerHTML = '✅ Copié ! Prêt à coller sur WhatsApp';
    setTimeout(() => { btn.innerHTML = oldText; }, 2000);
  });
}

function tickClock() {
  const now = new Date();
  document.getElementById('headerClock').innerText = now.toLocaleTimeString('fr-FR');
  if (currentMode === 'auto' && sessionActive) {
    calculate();
  }
}

loadState();
calculate();
setInterval(tickClock, 1000);
tickClock();
</script>
</body>
</html>
