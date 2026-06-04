# Pop-s-Workout-Program
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pete's Plan</title>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f5f2ec;
  --card: #ffffff;
  --ink: #1a1a18;
  --mid: #5a5a52;
  --faint: #e8e4db;
  --border: #ddd9cf;
  --fire: #e8440a;
  --amber: #d4820a;
  --green: #2a8a4a;
  --sky: #1a6fa8;
  --golf: #3a7a2a;
  --r: 14px;
}
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
html { font-size:16px; }
body {
  background: var(--bg);
  color: var(--ink);
  font-family: 'Sora', sans-serif;
  min-height: 100vh;
  max-width: 480px;
  margin: 0 auto;
}

/* ─── APP HEADER ─── */
.app-header {
  background: var(--ink);
  padding: 28px 24px 24px;
  position: sticky;
  top: 0;
  z-index: 100;
}
.app-header-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 18px;
}
.app-title {
  font-size: 26px;
  font-weight: 800;
  color: #fff;
  line-height: 1.1;
  letter-spacing: -0.02em;
}
.app-title span { color: var(--fire); }
.app-tagline {
  font-size: 11px;
  color: #888;
  font-family: 'JetBrains Mono', monospace;
  letter-spacing: 0.1em;
  margin-top: 4px;
}
.week-badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  background: rgba(255,255,255,0.1);
  color: #aaa;
  padding: 5px 10px;
  border-radius: 20px;
  letter-spacing: 0.08em;
}

/* Day Tabs */
.day-tabs {
  display: flex;
  gap: 6px;
  overflow-x: auto;
  scrollbar-width: none;
  padding-bottom: 2px;
}
.day-tabs::-webkit-scrollbar { display:none; }
.day-tab {
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  padding: 8px 12px;
  border-radius: 10px;
  cursor: pointer;
  border: 1px solid transparent;
  transition: all 0.18s ease;
  background: rgba(255,255,255,0.07);
}
.day-tab:hover { background: rgba(255,255,255,0.12); }
.day-tab.active {
  background: var(--fire);
  border-color: var(--fire);
}
.day-tab.rest-tab { opacity: 0.45; }
.day-tab.golf-tab.active { background: var(--golf); border-color: var(--golf); }
.tab-name {
  font-family: 'JetBrains Mono', monospace;
  font-size: 9px;
  font-weight: 500;
  letter-spacing: 0.1em;
  color: #aaa;
  text-transform: uppercase;
}
.day-tab.active .tab-name { color: #fff; }
.tab-dot {
  width: 5px; height: 5px;
  border-radius: 50%;
  background: #555;
}
.day-tab.active .tab-dot { background: rgba(255,255,255,0.7); }
.tab-type {
  font-size: 9.5px;
  font-weight: 600;
  color: #777;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}
.day-tab.active .tab-type { color: rgba(255,255,255,0.9); }

/* ─── MAIN CONTENT ─── */
.day-view { display: none; padding: 20px 16px 40px; }
.day-view.active { display: block; }

/* ─── DAY HERO CARD ─── */
.day-hero {
  background: var(--card);
  border-radius: var(--r);
  padding: 22px 20px;
  margin-bottom: 14px;
  border: 1px solid var(--border);
  position: relative;
  overflow: hidden;
}
.day-hero::before {
  content: '';
  position: absolute;
  top: 0; right: 0;
  width: 120px; height: 120px;
  border-radius: 50%;
  opacity: 0.06;
  transform: translate(30%, -30%);
}
.day-hero.type-strength::before { background: var(--sky); }
.day-hero.type-cardio::before { background: var(--fire); }
.day-hero.type-golf::before { background: var(--golf); }
.day-hero.type-rest::before { background: var(--mid); }

.day-hero-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 10px;
}
.day-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--mid);
  margin-bottom: 6px;
}
.day-title {
  font-size: 22px;
  font-weight: 800;
  letter-spacing: -0.02em;
  line-height: 1.15;
}
.type-badge {
  font-family: 'JetBrains Mono', monospace;
  font-size: 9px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 20px;
  font-weight: 500;
  flex-shrink: 0;
}
.badge-strength { background: rgba(26,111,168,0.1); color: var(--sky); border: 1px solid rgba(26,111,168,0.25); }
.badge-cardio { background: rgba(232,68,10,0.1); color: var(--fire); border: 1px solid rgba(232,68,10,0.25); }
.badge-golf { background: rgba(58,122,42,0.1); color: var(--golf); border: 1px solid rgba(58,122,42,0.25); }
.badge-rest { background: var(--faint); color: var(--mid); border: 1px solid var(--border); }
.badge-combo { background: rgba(212,130,10,0.1); color: var(--amber); border: 1px solid rgba(212,130,10,0.25); }

.day-meta {
  display: flex;
  gap: 16px;
  margin-top: 12px;
  padding-top: 12px;
  border-top: 1px solid var(--faint);
}
.meta-item { display: flex; flex-direction: column; gap: 2px; }
.meta-val { font-size: 15px; font-weight: 700; }
.meta-lbl { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--mid); letter-spacing: 0.08em; text-transform: uppercase; }

/* ─── SECTION HEADER ─── */
.section-head {
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--mid);
  margin: 20px 0 10px 4px;
}

/* ─── PHASE CARDS (cardio) ─── */
.phase-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 14px; }
.phase-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 14px 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.phase-info { display: flex; flex-direction: column; gap: 3px; }
.phase-name { font-weight: 600; font-size: 14px; }
.phase-detail { font-size: 12px; color: var(--mid); }
.phase-time {
  font-family: 'JetBrains Mono', monospace;
  font-size: 13px;
  font-weight: 500;
  color: var(--fire);
  white-space: nowrap;
  margin-left: 12px;
}

/* ─── EXERCISE CARDS ─── */
.exercise-list { display: flex; flex-direction: column; gap: 10px; }
.ex-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}
.ex-card-main {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 14px 16px;
  cursor: pointer;
  user-select: none;
}
.ex-num {
  width: 30px; height: 30px;
  border-radius: 8px;
  background: var(--faint);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 500;
  color: var(--mid);
  flex-shrink: 0;
}
.ex-info { flex: 1; min-width: 0; }
.ex-name { font-weight: 600; font-size: 14px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.ex-sets { font-size: 12px; color: var(--mid); margin-top: 2px; }
.ex-expand {
  font-size: 18px;
  color: var(--mid);
  transition: transform 0.2s;
  flex-shrink: 0;
}
.ex-card.open .ex-expand { transform: rotate(180deg); }
.ex-detail {
  display: none;
  padding: 0 16px 14px 60px;
  border-top: 1px solid var(--faint);
}
.ex-card.open .ex-detail { display: block; }
.ex-detail p { font-size: 13px; color: var(--mid); line-height: 1.65; padding-top: 12px; }
.ex-tip {
  display: flex;
  gap: 6px;
  margin-top: 8px;
  font-size: 12px;
  color: var(--amber);
  font-weight: 600;
  align-items: flex-start;
}
.weight-pill {
  display: inline-block;
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  background: var(--faint);
  color: var(--mid);
  padding: 2px 8px;
  border-radius: 8px;
  margin-top: 6px;
}

/* ─── CIRCUIT TIMER CARD ─── */
.circuit-card {
  background: var(--ink);
  border-radius: var(--r);
  padding: 20px;
  margin-bottom: 14px;
  color: #fff;
}
.circuit-title {
  font-family: 'JetBrains Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: #888;
  margin-bottom: 8px;
}
.circuit-body { font-size: 14px; color: #ccc; line-height: 1.6; }
.circuit-body strong { color: #fff; }

/* ─── AB TOGGLE ─── */
.ab-toggle {
  display: flex;
  background: var(--faint);
  border-radius: 10px;
  padding: 3px;
  margin-bottom: 14px;
  gap: 3px;
}
.ab-btn {
  flex: 1;
  text-align: center;
  padding: 9px;
  border-radius: 8px;
  font-weight: 700;
  font-size: 13px;
  cursor: pointer;
  transition: all 0.2s;
  color: var(--mid);
  border: none;
  background: transparent;
  font-family: 'Sora', sans-serif;
}
.ab-btn.active { background: var(--card); color: var(--ink); box-shadow: 0 1px 4px rgba(0,0,0,0.1); }

/* ─── INFO BOX ─── */
.info-box {
  background: var(--card);
  border: 1px solid var(--border);
  border-left: 3px solid var(--amber);
  border-radius: var(--r);
  padding: 16px 18px;
  margin-bottom: 12px;
  font-size: 13px;
  color: var(--mid);
  line-height: 1.65;
}
.info-box strong { color: var(--ink); }
.info-box.golf-box { border-left-color: var(--golf); }
.info-box.rest-box { border-left-color: var(--border); }

/* ─── CHECKLIST ─── */
.check-list { display: flex; flex-direction: column; gap: 8px; }
.check-item {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 12px 16px;
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  transition: background 0.15s;
}
.check-item:hover { background: var(--faint); }
.check-item.checked { opacity: 0.5; }
.check-box {
  width: 22px; height: 22px;
  border-radius: 6px;
  border: 2px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: all 0.15s;
}
.check-item.checked .check-box {
  background: var(--green);
  border-color: var(--green);
}
.check-icon { font-size: 13px; display: none; }
.check-item.checked .check-icon { display: block; }
.check-text { font-size: 13.5px; font-weight: 500; }

/* ─── GOLF VIEW ─── */
.golf-stat-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-bottom: 14px;
}
.golf-stat {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 16px;
}
.golf-stat-val { font-size: 22px; font-weight: 800; color: var(--golf); }
.golf-stat-lbl { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--mid); letter-spacing: 0.1em; text-transform: uppercase; margin-top: 3px; }

/* ─── REST DAY ─── */
.rest-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.rest-card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 16px;
}
.rest-card .rest-icon { font-size: 24px; margin-bottom: 8px; }
.rest-card h4 { font-size: 13px; font-weight: 700; margin-bottom: 4px; }
.rest-card p { font-size: 12px; color: var(--mid); line-height: 1.55; }

/* ─── PROGRESS BUTTON ─── */
.done-btn {
  width: 100%;
  background: var(--fire);
  color: #fff;
  border: none;
  border-radius: 12px;
  padding: 16px;
  font-family: 'Sora', sans-serif;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
  margin-top: 20px;
  letter-spacing: 0.01em;
  transition: opacity 0.15s;
}
.done-btn:hover { opacity: 0.9; }
.done-btn.golf-btn { background: var(--golf); }
.done-btn.rest-btn { background: var(--mid); }

/* ─── TOAST ─── */
.toast {
  position: fixed;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%) translateY(80px);
  background: var(--ink);
  color: #fff;
  padding: 13px 24px;
  border-radius: 30px;
  font-size: 14px;
  font-weight: 600;
  z-index: 999;
  transition: transform 0.35s cubic-bezier(0.34,1.56,0.64,1);
  white-space: nowrap;
}
.toast.show { transform: translateX(-50%) translateY(0); }

/* Animation */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}
.day-view.active > * {
  animation: fadeUp 0.3s ease both;
}
.day-view.active > *:nth-child(1) { animation-delay: 0.03s; }
.day-view.active > *:nth-child(2) { animation-delay: 0.07s; }
.day-view.active > *:nth-child(3) { animation-delay: 0.11s; }
.day-view.active > *:nth-child(4) { animation-delay: 0.15s; }
.day-view.active > *:nth-child(5) { animation-delay: 0.19s; }
</style>
</head>
<body>

<div class="app-header">
  <div class="app-header-top">
    <div>
      <div class="app-title">Pete's<br><span>Game Plan</span></div>
      <div class="app-tagline">// AGE 58 · BUILT TO LAST</div>
    </div>
    <div class="week-badge">WEEK 1</div>
  </div>
  <div class="day-tabs" id="dayTabs">
    <div class="day-tab active" data-day="mon">
      <div class="tab-name">MON</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Workout A</div>
    </div>
    <div class="day-tab" data-day="tue">
      <div class="tab-name">TUE</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Cardio</div>
    </div>
    <div class="day-tab" data-day="wed">
      <div class="tab-name">WED</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Workout B</div>
    </div>
    <div class="day-tab" data-day="thu">
      <div class="tab-name">THU</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Rest</div>
    </div>
    <div class="day-tab" data-day="fri">
      <div class="tab-name">FRI</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Workout A</div>
    </div>
    <div class="day-tab golf-tab" data-day="sat">
      <div class="tab-name">SAT</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Golf ⛳</div>
    </div>
    <div class="day-tab rest-tab" data-day="sun">
      <div class="tab-name">SUN</div>
      <div class="tab-dot"></div>
      <div class="tab-type">Rest</div>
    </div>
  </div>
</div>

<!-- ════════ MONDAY ════════ -->
<div class="day-view active" id="day-mon">
  <div class="day-hero type-strength">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Monday</div>
        <div class="day-title">Workout A<br>Full Body</div>
      </div>
      <span class="type-badge badge-strength">STRENGTH + CARDIO</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">35–40</div><div class="meta-lbl">Minutes</div></div>
      <div class="meta-item"><div class="meta-val">5</div><div class="meta-lbl">Exercises</div></div>
      <div class="meta-item"><div class="meta-val">Full</div><div class="meta-lbl">Body</div></div>
    </div>
  </div>

  <div class="circuit-card">
    <div class="circuit-title">// THE STRUCTURE</div>
    <div class="circuit-body">
      <strong>5 min</strong> treadmill warm-up walk →
      <strong>5 rounds</strong> of the circuit below, rest 60 sec between rounds →
      <strong>5 min</strong> cool-down stretch. No rest between exercises inside a round.
    </div>
  </div>

  <div class="section-head">// The Circuit — Round x5</div>
  <div class="exercise-list">
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">01</div>
        <div class="ex-info">
          <div class="ex-name">Goblet Squat</div>
          <div class="ex-sets">10 reps · 35–45 lb</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Hold one dumbbell at your chest. Feet shoulder-width, toes slightly out. Squat deep, keep chest tall, drive through the heels to stand.</p>
        <p class="ex-tip">⚡ The single best leg exercise for your knees and lower back at this age. These are your fat-burning engine — don't skip them.</p>
        <div class="weight-pill">START: 35 lb → BUILD TO: 50 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">02</div>
        <div class="ex-info">
          <div class="ex-name">Dumbbell Chest Press</div>
          <div class="ex-sets">10 reps · 30–40 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Lie on the floor. Dumbbells at chest level, elbows at 45°. Press up slowly (3 sec down, 1 sec up). Floor press is safer on the shoulder joint than a full bench.</p>
        <div class="weight-pill">START: 30 lb → BUILD TO: 40 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">03</div>
        <div class="ex-info">
          <div class="ex-name">Bent-Over Row</div>
          <div class="ex-sets">10 reps · 30–45 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Hinge forward at the hips, flat back, arms hang down. Pull elbows back hard — squeeze 1 full second at the top. This builds the back that protects your spine and makes you look powerful from behind.</p>
        <p class="ex-tip">⚡ Form cue: Think "elbows to back pockets." Never let the back round.</p>
        <div class="weight-pill">START: 30 lb → BUILD TO: 45 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">04</div>
        <div class="ex-info">
          <div class="ex-name">Dumbbell Shoulder Press</div>
          <div class="ex-sets">10 reps · 20–30 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Standing. Dumbbells at ear level, press straight up. Don't lock out the elbows at the top. Builds the shoulder width and strength that men lose fastest after 55.</p>
        <div class="weight-pill">START: 20 lb → BUILD TO: 30 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">05</div>
        <div class="ex-info">
          <div class="ex-name">Plank Hold</div>
          <div class="ex-sets">45 seconds</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Forearms on the floor, body straight from head to heel. Squeeze your glutes. Don't let the hips sag or pike. This builds the functional core that flattens your midsection from the inside — far more effective than crunches.</p>
        <p class="ex-tip">⚡ Progress by adding 5 seconds every week until you hit 90 seconds.</p>
      </div>
    </div>
  </div>

  <div class="section-head">// Today's Checklist</div>
  <div class="check-list" id="check-mon">
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min treadmill warm-up</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 rounds of the circuit</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Drank water before & after</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min cool-down stretch</div></div>
  </div>
  <button class="done-btn" onclick="markDone('Monday')">Mark Monday Complete ✓</button>
</div>

<!-- ════════ TUESDAY ════════ -->
<div class="day-view" id="day-tue">
  <div class="day-hero type-cardio">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Tuesday</div>
        <div class="day-title">Zone 2<br>Cardio</div>
      </div>
      <span class="type-badge badge-cardio">FAT BURN</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">35</div><div class="meta-lbl">Minutes</div></div>
      <div class="meta-item"><div class="meta-val">60–70%</div><div class="meta-lbl">Max HR</div></div>
      <div class="meta-item"><div class="meta-val">Low</div><div class="meta-lbl">Intensity</div></div>
    </div>
  </div>

  <div class="info-box">
    <strong>Why Zone 2?</strong> This is the primary fat-burning zone — your body uses stored fat (not sugar) as fuel here. 35 minutes at this effort burns more visceral fat over time than harder cardio. You should be able to hold a full conversation the entire time.
  </div>

  <div class="section-head">// Pick Your Machine</div>

  <div class="ab-toggle" id="cardio-toggle">
    <button class="ab-btn active" onclick="switchCardio('peloton')">🚴 Peloton</button>
    <button class="ab-btn" onclick="switchCardio('treadmill')">🏃 Treadmill</button>
  </div>

  <div id="cardio-peloton">
    <div class="phase-list">
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Warm-Up</div><div class="phase-detail">Easy spin, resistance 20–25</div></div><div class="phase-time">5 MIN</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Zone 2 Ride</div><div class="phase-detail">Resistance 35–45 · 70–80 RPM · conversational pace</div></div><div class="phase-time">25 MIN</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Cool-Down</div><div class="phase-detail">Gentle spin, drop resistance</div></div><div class="phase-time">5 MIN</div></div>
    </div>
  </div>
  <div id="cardio-treadmill" style="display:none">
    <div class="phase-list">
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Warm-Up</div><div class="phase-detail">Flat walk, 3.0 mph</div></div><div class="phase-time">5 MIN</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Incline Walk</div><div class="phase-detail">3.0–3.5 mph · 6–8% incline</div></div><div class="phase-time">25 MIN</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Cool-Down</div><div class="phase-detail">Flat walk, drop to 2.5 mph</div></div><div class="phase-time">5 MIN</div></div>
    </div>
  </div>

  <div class="section-head">// Today's Checklist</div>
  <div class="check-list">
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">35 minutes complete</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Could hold a conversation throughout</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Drank water before & after</div></div>
  </div>
  <button class="done-btn" onclick="markDone('Tuesday')">Mark Tuesday Complete ✓</button>
</div>

<!-- ════════ WEDNESDAY ════════ -->
<div class="day-view" id="day-wed">
  <div class="day-hero type-strength">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Wednesday</div>
        <div class="day-title">Workout B<br>Full Body</div>
      </div>
      <span class="type-badge badge-combo">STRENGTH + HIIT</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">40–45</div><div class="meta-lbl">Minutes</div></div>
      <div class="meta-item"><div class="meta-val">5</div><div class="meta-lbl">Exercises</div></div>
      <div class="meta-item"><div class="meta-val">+ Intervals</div><div class="meta-lbl">Finisher</div></div>
    </div>
  </div>

  <div class="circuit-card">
    <div class="circuit-title">// THE STRUCTURE</div>
    <div class="circuit-body">
      <strong>5 min</strong> warm-up →
      <strong>4 rounds</strong> of the circuit below, 60 sec rest between rounds →
      <strong>10 min HIIT finisher</strong> on Peloton or treadmill →
      <strong>5 min</strong> stretch.
    </div>
  </div>

  <div class="section-head">// Circuit — 4 Rounds (Different from Monday)</div>
  <div class="exercise-list">
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">01</div>
        <div class="ex-info">
          <div class="ex-name">Romanian Deadlift</div>
          <div class="ex-sets">10 reps · 30–45 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Hinge at hips, soft knee bend, lower dumbbells along your legs until you feel the hamstring stretch — then drive hips forward to stand. Builds the entire back of the body and protects the lower back.</p>
        <p class="ex-tip">⚡ If your back rounds at all, the weight is too heavy. Drop down and do it right.</p>
        <div class="weight-pill">START: 30 lb → BUILD TO: 45 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">02</div>
        <div class="ex-info">
          <div class="ex-name">Single-Arm Row</div>
          <div class="ex-sets">10 reps each side · 35–50 lb</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Brace one hand on a table or chair. Other hand holds a dumbbell. Pull elbow up and back hard — the lat and mid-back do the work, not the arm. Fixes any left-right imbalances from years of one-sided activity.</p>
        <div class="weight-pill">START: 35 lb → BUILD TO: 50 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">03</div>
        <div class="ex-info">
          <div class="ex-name">Reverse Lunge</div>
          <div class="ex-sets">10 reps each leg · 20–30 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Step backward (not forward) — drop the back knee toward the floor, front knee stays over the ankle, then push off the front foot to return. Reverse lunges are far gentler on the knee joint than forward lunges.</p>
        <div class="weight-pill">START: 20 lb → BUILD TO: 30 lb</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">04</div>
        <div class="ex-info">
          <div class="ex-name">Lateral Raise</div>
          <div class="ex-sets">12 reps · 10–15 lb each</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Slight forward lean, arms slightly bent, raise out to the sides slowly — lower even slower (3 sec down). Builds the lateral shoulder cap that creates width. Do NOT swing the weight up.</p>
        <div class="weight-pill">STAY AT: 10–15 lb · Slow & controlled always</div>
      </div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main">
        <div class="ex-num">05</div>
        <div class="ex-info">
          <div class="ex-name">Dead Bug</div>
          <div class="ex-sets">8 reps each side · bodyweight</div>
        </div>
        <div class="ex-expand">⌄</div>
      </div>
      <div class="ex-detail">
        <p>Lie on back. Arms straight up, knees at 90°. Slowly lower opposite arm and leg toward the floor — hold 2 sec — return. Lower back stays pressed into the floor the entire time. The best spinal stability exercise that exists.</p>
      </div>
    </div>
  </div>

  <div class="section-head">// 10-Min HIIT Finisher</div>
  <div class="ab-toggle" id="hiit-toggle">
    <button class="ab-btn active" onclick="switchHiit('peloton')">🚴 Peloton</button>
    <button class="ab-btn" onclick="switchHiit('treadmill')">🏃 Treadmill</button>
  </div>
  <div id="hiit-peloton">
    <div class="phase-list">
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Sprint</div><div class="phase-detail">High resistance · max effort</div></div><div class="phase-time">30 SEC</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Recover</div><div class="phase-detail">Easy pedal · low resistance</div></div><div class="phase-time">90 SEC</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Repeat</div><div class="phase-detail">Sprint / Recover cycle</div></div><div class="phase-time">5 ROUNDS</div></div>
    </div>
  </div>
  <div id="hiit-treadmill" style="display:none">
    <div class="phase-list">
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Fast Walk / Jog</div><div class="phase-detail">5.5–7.0 mph · hard effort</div></div><div class="phase-time">45 SEC</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Recover Walk</div><div class="phase-detail">3.0 mph · flat</div></div><div class="phase-time">90 SEC</div></div>
      <div class="phase-card"><div class="phase-info"><div class="phase-name">Repeat</div><div class="phase-detail">Run / Walk cycle</div></div><div class="phase-time">5 ROUNDS</div></div>
    </div>
  </div>

  <div class="section-head">// Today's Checklist</div>
  <div class="check-list">
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min warm-up</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">4 rounds of circuit B</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">10 min HIIT finisher</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Drank water before & after</div></div>
  </div>
  <button class="done-btn" onclick="markDone('Wednesday')">Mark Wednesday Complete ✓</button>
</div>

<!-- ════════ THURSDAY ════════ -->
<div class="day-view" id="day-thu">
  <div class="day-hero type-rest">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Thursday</div>
        <div class="day-title">Recovery<br>Day</div>
      </div>
      <span class="type-badge badge-rest">ACTIVE REST</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">Optional</div><div class="meta-lbl">Walk only</div></div>
      <div class="meta-item"><div class="meta-val">Low</div><div class="meta-lbl">Intensity</div></div>
    </div>
  </div>

  <div class="info-box rest-box">
    <strong>Rest is part of the program.</strong> Muscle isn't built during the workout — it's built during recovery. Thursday exists so Friday is high quality. Don't feel guilty about this day. Your body needs it.
  </div>

  <div class="section-head">// What to Do Today</div>
  <div class="rest-grid">
    <div class="rest-card"><div class="rest-icon">🚶</div><h4>Optional Walk</h4><p>20–30 min easy walk outside. Not a workout — just movement to keep blood flowing.</p></div>
    <div class="rest-card"><div class="rest-icon">🧘</div><h4>Stretch</h4><p>10 min hip flexors, hamstrings, chest, and shoulders. YouTube "5 min full body stretch."</p></div>
    <div class="rest-card"><div class="rest-icon">💧</div><h4>Hydrate</h4><p>Still hit 80 oz of water today. Recovery is built on hydration and sleep.</p></div>
    <div class="rest-card"><div class="rest-icon">🥩</div><h4>Protein</h4><p>Don't skip protein just because you're resting. Muscle repair is happening today.</p></div>
  </div>
  <button class="done-btn rest-btn" onclick="markDone('Thursday')">Mark Thursday Complete ✓</button>
</div>

<!-- ════════ FRIDAY ════════ -->
<div class="day-view" id="day-fri">
  <div class="day-hero type-strength">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Friday</div>
        <div class="day-title">Workout A<br>Full Body</div>
      </div>
      <span class="type-badge badge-strength">STRENGTH + CARDIO</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">35–40</div><div class="meta-lbl">Minutes</div></div>
      <div class="meta-item"><div class="meta-val">5</div><div class="meta-lbl">Exercises</div></div>
      <div class="meta-item"><div class="meta-val">5 Rounds</div><div class="meta-lbl">Circuit</div></div>
    </div>
  </div>

  <div class="circuit-card">
    <div class="circuit-title">// SAME AS MONDAY — BEAT YOUR WEIGHTS</div>
    <div class="circuit-body">
      Same Workout A circuit. The goal is simple: <strong>go slightly heavier</strong> on at least one exercise compared to Monday. Even 5 lbs more on one movement counts as a win. That's how progress happens.
    </div>
  </div>

  <div class="section-head">// The Circuit — 5 Rounds (Same as Monday)</div>
  <div class="exercise-list">
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main"><div class="ex-num">01</div><div class="ex-info"><div class="ex-name">Goblet Squat</div><div class="ex-sets">10 reps · Match or beat Monday</div></div><div class="ex-expand">⌄</div></div>
      <div class="ex-detail"><p>Hold one dumbbell at chest. Deep squat, chest tall, drive through heels. Did you use 35 lb Monday? Try 40 lb for at least 2 rounds.</p></div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main"><div class="ex-num">02</div><div class="ex-info"><div class="ex-name">Dumbbell Chest Press</div><div class="ex-sets">10 reps · Match or beat Monday</div></div><div class="ex-expand">⌄</div></div>
      <div class="ex-detail"><p>Floor press. 3-second descent. Same focus on control as Monday. Add 5 lbs if the last 3 reps felt easy on Monday.</p></div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main"><div class="ex-num">03</div><div class="ex-info"><div class="ex-name">Bent-Over Row</div><div class="ex-sets">10 reps · Match or beat Monday</div></div><div class="ex-expand">⌄</div></div>
      <div class="ex-detail"><p>Elbows to back pockets. Flat back. Squeeze 1 full second at the top. This is the most important exercise in the program — make it count.</p></div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main"><div class="ex-num">04</div><div class="ex-info"><div class="ex-name">Shoulder Press</div><div class="ex-sets">10 reps · Match or beat Monday</div></div><div class="ex-expand">⌄</div></div>
      <div class="ex-detail"><p>Standing. Press straight up. Match Monday's weight and focus on clean, controlled form before jumping up in weight here.</p></div>
    </div>
    <div class="ex-card" onclick="toggleEx(this)">
      <div class="ex-card-main"><div class="ex-num">05</div><div class="ex-info"><div class="ex-name">Plank Hold</div><div class="ex-sets">45–60 seconds</div></div><div class="ex-expand">⌄</div></div>
      <div class="ex-detail"><p>Add 5–10 seconds to Monday's hold time. That's the only goal. Glutes squeezed, don't let hips drop.</p></div>
    </div>
  </div>

  <div class="section-head">// Today's Checklist</div>
  <div class="check-list">
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min treadmill warm-up</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 rounds complete</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Beat at least one weight from Monday</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min cool-down stretch</div></div>
  </div>
  <button class="done-btn" onclick="markDone('Friday')">Mark Friday Complete ✓</button>
</div>

<!-- ════════ SATURDAY (GOLF) ════════ -->
<div class="day-view" id="day-sat">
  <div class="day-hero type-golf">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Saturday</div>
        <div class="day-title">Golf Day ⛳<br>Walk the 18</div>
      </div>
      <span class="type-badge badge-golf">ACTIVE CARDIO</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">4–5</div><div class="meta-lbl">Miles</div></div>
      <div class="meta-item"><div class="meta-val">10,000+</div><div class="meta-lbl">Steps</div></div>
      <div class="meta-item"><div class="meta-val">No Cart</div><div class="meta-lbl">Rule</div></div>
    </div>
  </div>

  <div class="info-box golf-box">
    <strong>This counts as a full workout day.</strong> Walking 18 holes burns 1,200–1,500 calories, logs 4–5 miles of Zone 2 cardio, and puts a fraction of the joint stress of running. This is the most sustainable cardio activity on his schedule — and the fact that he loves it is the biggest advantage of all.
  </div>

  <div class="section-head">// The One Rule</div>
  <div class="circuit-card">
    <div class="circuit-title">// NO CART — NO EXCEPTIONS</div>
    <div class="circuit-body">
      Walking is the exercise. The cart is the enemy. Carry or push the bag. Every hole walked is Zone 2 cardio that directly attacks visceral fat. This is the <strong>most enjoyable thing</strong> on the weekly plan — protect it.
    </div>
  </div>

  <div class="golf-stat-row">
    <div class="golf-stat"><div class="golf-stat-val">~1,400</div><div class="golf-stat-lbl">Calories burned</div></div>
    <div class="golf-stat"><div class="golf-stat-val">3–4 hrs</div><div class="golf-stat-lbl">Active time</div></div>
    <div class="golf-stat"><div class="golf-stat-val">Zone 2</div><div class="golf-stat-lbl">Intensity = fat burn</div></div>
    <div class="golf-stat"><div class="golf-stat-val">0</div><div class="golf-stat-lbl">Joint stress vs. running</div></div>
  </div>

  <div class="section-head">// Pre-Round Prep (10 min)</div>
  <div class="check-list">
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">16 oz water before leaving</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">5 min hip flexor + shoulder stretch</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Walked all 18 (no cart)</div></div>
    <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"><div class="check-icon">✓</div></div><div class="check-text">Rehydrated after the round</div></div>
  </div>
  <button class="done-btn golf-btn" onclick="markDone('Saturday')">Mark Saturday Complete ⛳</button>
</div>

<!-- ════════ SUNDAY ════════ -->
<div class="day-view" id="day-sun">
  <div class="day-hero type-rest">
    <div class="day-hero-top">
      <div>
        <div class="day-label">Sunday</div>
        <div class="day-title">Full Rest<br>Day</div>
      </div>
      <span class="type-badge badge-rest">RECOVERY</span>
    </div>
    <div class="day-meta">
      <div class="meta-item"><div class="meta-val">0</div><div class="meta-lbl">Workouts</div></div>
      <div class="meta-item"><div class="meta-val">7–8 hrs</div><div class="meta-lbl">Sleep target</div></div>
    </div>
  </div>

  <div class="info-box rest-box">
    <strong>Do nothing.</strong> No cardio, no weights, no guilt. Growth hormone — the hormone that drives fat loss and muscle repair — is released almost entirely during deep sleep. Sunday's job is to sleep well and eat well.
  </div>

  <div class="section-head">// Sunday Is For</div>
  <div class="rest-grid">
    <div class="rest-card"><div class="rest-icon">😴</div><h4>Sleep</h4><p>7–8 hours. Non-negotiable. More important than any single workout for fat loss at 58.</p></div>
    <div class="rest-card"><div class="rest-icon">🥗</div><h4>Meal Prep</h4><p>Set up proteins for the week: hard-boiled eggs, grilled chicken, Greek yogurt stocked.</p></div>
    <div class="rest-card"><div class="rest-icon">📏</div><h4>Waist Check</h4><p>Measure waist at navel once per Sunday, fasted. Write it down. That's the number that matters.</p></div>
    <div class="rest-card"><div class="rest-icon">💪</div><h4>Plan Next Week</h4><p>Look at the plan Monday–Friday. Commit to the schedule before the week starts.</p></div>
  </div>
  <button class="done-btn rest-btn" onclick="markDone('Sunday')">Start a New Week →</button>
</div>

<!-- Toast -->
<div class="toast" id="toast"></div>

<script>
// Tab switching
document.getElementById('dayTabs').addEventListener('click', function(e) {
  const tab = e.target.closest('.day-tab');
  if (!tab) return;
  const day = tab.dataset.day;
  document.querySelectorAll('.day-tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.day-view').forEach(v => v.classList.remove('active'));
  tab.classList.add('active');
  document.getElementById('day-' + day).classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
});

// Exercise expand/collapse
function toggleEx(card) {
  card.classList.toggle('open');
}

// Check items
function toggleCheck(item) {
  item.classList.toggle('checked');
}

// Cardio machine toggle
function switchCardio(type) {
  document.querySelectorAll('#cardio-toggle .ab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('cardio-peloton').style.display = type === 'peloton' ? 'block' : 'none';
  document.getElementById('cardio-treadmill').style.display = type === 'treadmill' ? 'block' : 'none';
  event.target.classList.add('active');
}

// HIIT toggle
function switchHiit(type) {
  document.querySelectorAll('#hiit-toggle .ab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('hiit-peloton').style.display = type === 'peloton' ? 'block' : 'none';
  document.getElementById('hiit-treadmill').style.display = type === 'treadmill' ? 'block' : 'none';
  event.target.classList.add('active');
}

// Done button / toast
function markDone(day) {
  const msgs = {
    'Monday': '💪 Monday done. Two down this week.',
    'Tuesday': '🔥 Cardio checked. Fat burning mode activated.',
    'Wednesday': '⚡ Workout B complete. Strong work.',
    'Thursday': '✅ Rest day done right.',
    'Friday': '🏆 Week complete. Take the weekend.',
    'Saturday': '⛳ 18 holes walked. That\'s a workout.',
    'Sunday': '🌅 New week starts tomorrow. Let\'s go.'
  };
  showToast(msgs[day] || 'Day complete!');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}
</script>
</body>
</html>
