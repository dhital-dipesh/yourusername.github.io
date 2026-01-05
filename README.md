# yourusername.github.io<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Calm Study — Dipesh</title>
  <style>
    :root {
      --bg: #0b1020;
      --card: rgba(255,255,255,0.06);
      --text: #e8eefc;
      --muted: rgba(232,238,252,0.75);
      --accent: rgba(120, 180, 255, 0.9);
      --border: rgba(255,255,255,0.10);
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 600px at 20% 10%, rgba(120,180,255,0.18), transparent 55%),
                  radial-gradient(1000px 500px at 80% 20%, rgba(180,120,255,0.12), transparent 60%),
                  var(--bg);
      color: var(--text);
      min-height: 100vh;
      display: grid;
      place-items: center;
      padding: 24px;
      overflow-x: hidden;
    }
    .wrap {
      width: min(980px, 100%);
      display: grid;
      gap: 16px;
    }
    .top {
      display: flex;
      gap: 16px;
      flex-wrap: wrap;
      align-items: stretch;
    }
    .card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 18px;
      backdrop-filter: blur(10px);
      box-shadow: 0 12px 30px rgba(0,0,0,0.35);
    }
    .card h2 {
      margin: 0 0 10px 0;
      font-size: 16px;
      letter-spacing: 0.2px;
      color: var(--muted);
      font-weight: 600;
    }
    .timeBox { flex: 1 1 280px; }
    .timerBox { flex: 1 1 320px; }
    .astroBox { flex: 1 1 320px; }
    .big {
      font-size: 30px;
      font-weight: 750;
      letter-spacing: 0.3px;
      margin: 6px 0 0 0;
    }
    .muted { color: var(--muted); }
    .row { display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }
    input, select, button {
      border-radius: 12px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.06);
      color: var(--text);
      padding: 10px 12px;
      font-size: 14px;
      outline: none;
    }
    input::placeholder { color: rgba(232,238,252,0.45); }
    button {
      cursor: pointer;
      transition: transform 0.05s ease, background 0.2s ease;
    }
    button:hover { background: rgba(255,255,255,0.10); }
    button:active { transform: translateY(1px); }
    .btnPrimary {
      border-color: rgba(120,180,255,0.35);
      background: rgba(120,180,255,0.18);
    }
    .pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 12px;
      border-radius: 999px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.05);
      color: var(--muted);
      font-size: 13px;
    }
    .grid2 {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }
    @media (max-width: 820px) {
      .grid2 { grid-template-columns: 1fr; }
    }

    /* Meteor overlay */
    .overlay {
      position: fixed;
      inset: 0;
      background: radial-gradient(1000px 600px at 50% 40%, rgba(255,255,255,0.08), rgba(0,0,0,0.65));
      display: grid;
      place-items: center;
      z-index: 9999;
      pointer-events: none;
      opacity: 1;
      transition: opacity 900ms ease;
    }
    .overlay.hidden { opacity: 0; }
    .overlay .label {
      position: relative;
      z-index: 2;
      text-align: center;
      padding: 18px 20px;
      border-radius: 18px;
      border: 1px solid rgba(255,255,255,0.14);
      background: rgba(10,16,32,0.35);
      backdrop-filter: blur(10px);
      box-shadow: 0 16px 35px rgba(0,0,0,0.45);
    }
    .overlay .label .title { font-size: 18px; font-weight: 700; }
    .overlay .label .sub { font-size: 13px; color: var(--muted); margin-top: 6px; }

    .sky {
      position: absolute;
      inset: 0;
      overflow: hidden;
      z-index: 1;
    }
    .meteor {
      position: absolute;
      top: -10%;
      left: 110%;
      width: 220px;
      height: 2px;
      background: linear-gradient(90deg, rgba(255,255,255,0), rgba(255,255,255,0.95), rgba(255,255,255,0));
      filter: drop-shadow(0 0 8px rgba(255,255,255,0.6));
      transform: rotate(-22deg);
      animation: fly 1.8s linear forwards;
      opacity: 0.9;
    }
    @keyframes fly {
      from { transform: translate(0,0) rotate(-22deg); opacity: 0.0; }
      10% { opacity: 1; }
      to { transform: translate(-160vw, 120vh) rotate(-22deg); opacity: 0; }
    }
  </style>
</head>
<body>
  <!-- Meteor Shower Intro -->
  <div id="overlay" class="overlay">
    <div class="sky" id="sky"></div>
    <div class="label">
      <div class="title">Breathe in. Focus out.</div>
      <div class="sub">Calm start — meteor shower mode ✨</div>
    </div>
  </div>

  <div class="wrap">
    <div class="top">
      <div class="card timeBox">
        <h2>Today</h2>
        <div class="pill">📍 Japan (Asia/Tokyo)</div>
        <div class="big" id="clock">--:--:--</div>
        <div class="muted" id="dateLine">---</div>
      </div>

      <div class="card timerBox">
        <h2>Study Countdown</h2>
        <div class="big" id="timerDisplay">25:00</div>
        <div class="row" style="margin-top:10px;">
          <button class="btnPrimary" id="startBtn">Start</button>
          <button id="pauseBtn">Pause</button>
          <button id="resetBtn">Reset</button>
        </div>
        <div class="row" style="margin-top:12px;">
          <span class="muted">Preset:</span>
          <select id="preset">
            <option value="1500">Pomodoro 25:00</option>
            <option value="3000">Deep Focus 50:00</option>
            <option value="900">Quick 15:00</option>
            <option value="600">Warm-up 10:00</option>
          </select>
          <button id="applyPreset">Apply</button>
        </div>
        <div class="muted" style="margin-top:10px;">
          Tip: keep this tab open while studying. Simple. Quiet. No distractions.
        </div>
      </div>

      <div class="card astroBox">
        <h2>Horoscope (Date & Time)</h2>
        <div class="grid2">
          <div>
            <div class="muted" style="margin-bottom:6px;">Your birth date</div>
            <input id="birthDate" type="date" />
          </div>
          <div>
            <div class="muted" style="margin-bottom:6px;">Birth time (optional)</div>
            <input id="birthTime" type="time" />
          </div>
        </div>
        <div class="row" style="margin-top:12px;">
          <button class="btnPrimary" id="saveAstro">Save</button>
          <button id="clearAstro">Clear</button>
        </div>

        <div style="margin-top:14px;">
          <div class="pill">♈♉♊♋♌♍♎♏♐♑♒♓</div>
          <div class="big" id="zodiac">Zodiac: —</div>
          <div class="muted" id="horoscopeText" style="margin-top:6px;">
            Add your birth date to see your sign and a calm “study vibe” message.
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <h2>Calm Mode</h2>
      <div class="muted">
        “Small steps, every day.”  
        If you want, I can add: soothing background stars, lo-fi playlist links, or a goal tracker (still free).
      </div>
    </div>
  </div>

  <script>
    // ---------- Clock (Tokyo) ----------
    const clockEl = document.getElementById("clock");
    const dateLineEl = document.getElementById("dateLine");

    function tickClock() {
      const now = new Date();
      const fmtTime = new Intl.DateTimeFormat("en-GB", {
        timeZone: "Asia/Tokyo",
        hour: "2-digit", minute: "2-digit", second: "2-digit"
      }).format(now);

      const fmtDate = new Intl.DateTimeFormat("en-US", {
        timeZone: "Asia/Tokyo",
        weekday: "long", year: "numeric", month: "long", day: "numeric"
      }).format(now);

      clockEl.textContent = fmtTime;
      dateLineEl.textContent = fmtDate;
    }
    tickClock();
    setInterval(tickClock, 1000);

    // ---------- Study Timer ----------
    let totalSeconds = 1500;
    let remaining = totalSeconds;
    let running = false;
    let intervalId = null;

    const timerDisplay = document.getElementById("timerDisplay");
    const startBtn = document.getElementById("startBtn");
    const pauseBtn = document.getElementById("pauseBtn");
    const resetBtn = document.getElementById("resetBtn");
    const preset = document.getElementById("preset");
    const applyPreset = document.getElementById("applyPreset");

    function formatMMSS(s) {
      const m = Math.floor(s / 60);
      const sec = s % 60;
      return String(m).padStart(2, "0") + ":" + String(sec).padStart(2, "0");
    }
    function renderTimer() {
      timerDisplay.textContent = formatMMSS(remaining);
      document.title = (running ? "⏳ " : "") + formatMMSS(remaining) + " • Calm Study";
    }
    function startTimer() {
      if (running) return;
      running = true;
      intervalId = setInterval(() => {
        if (remaining > 0) {
          remaining -= 1;
          renderTimer();
        } else {
          stopTimer();
          // gentle finish
          alert("✅ Session done. Take a short break (water + deep breath).");
        }
      }, 1000);
      renderTimer();
    }
    function stopTimer() {
      running = false;
      if (intervalId) clearInterval(intervalId);
      intervalId = null;
      renderTimer();
    }
    function resetTimer() {
      stopTimer();
      remaining = totalSeconds;
      renderTimer();
    }

    startBtn.addEventListener("click", startTimer);
    pauseBtn.addEventListener("click", stopTimer);
    resetBtn.addEventListener("click", resetTimer);
    applyPreset.addEventListener("click", () => {
      totalSeconds = parseInt(preset.value, 10);
      remaining = totalSeconds;
      renderTimer();
    });

    renderTimer();

    // ---------- Horoscope (Zodiac from birth date) ----------
    const birthDate = document.getElementById("birthDate");
    const birthTime = document.getElementById("birthTime");
    const saveAstro = document.getElementById("saveAstro");
    const clearAstro = document.getElementById("clearAstro");
    const zodiacEl = document.getElementById("zodiac");
    const horoscopeText = document.getElementById("horoscopeText");

    function getZodiac(month, day) {
      // month: 1-12
      const z = [
        ["Capricorn", 1, 19],
        ["Aquarius", 2, 18],
        ["Pisces", 3, 20],
        ["Aries", 4, 19],
        ["Taurus", 5, 20],
        ["Gemini", 6, 20],
        ["Cancer", 7, 22],
        ["Leo", 8, 22],
        ["Virgo", 9, 22],
        ["Libra", 10, 22],
        ["Scorpio", 11, 21],
        ["Sagittarius", 12, 21],
        ["Capricorn", 12, 31],
      ];
      // Determine sign by boundaries
      for (let i = 0; i < z.length - 1; i++) {
        const [name, m, d] = z[i];
        const [nextName, nm, nd] = z[i + 1];
        // If before boundary of current sign -> previous
        // We'll check the upper boundary defined by each sign end date
      }
      // Simpler: use standard date ranges
      const ranges = [
        ["Capricorn", 12, 22, 1, 19],
        ["Aquarius", 1, 20, 2, 18],
        ["Pisces", 2, 19, 3, 20],
        ["Aries", 3, 21, 4, 19],
        ["Taurus", 4, 20, 5, 20],
        ["Gemini", 5, 21, 6, 20],
        ["Cancer", 6, 21, 7, 22],
        ["Leo", 7, 23, 8, 22],
        ["Virgo", 8, 23, 9, 22],
        ["Libra", 9, 23, 10, 22],
        ["Scorpio", 10, 23, 11, 21],
        ["Sagittarius", 11, 22, 12, 21],
      ];
      for (const [name, sm, sd, em, ed] of ranges) {
        if (
          (month === sm && day >= sd) ||
          (month === em && day <= ed) ||
          (sm > em && (month === sm && day >= sd) || (month === em && day <= ed)) // Capricorn wrap handled separately
        ) {
          return name;
        }
      }
      // Capricorn wrap:
      if ((month === 12 && day >= 22) || (month === 1 && day <= 19)) return "Capricorn";
      return "—";
    }

    function calmMessage(sign, timeStr) {
      // Not “real astrology predictions” — just calming study vibes.
      const base = {
        Aries: "Start fast, then slow down. One problem at a time.",
        Taurus: "Consistency wins today. Keep it steady and simple.",
        Gemini: "Clear your desk, clear your mind. Focus on one topic.",
        Cancer: "Gentle rhythm. Review basics, then build confidence.",
        Leo: "Show up like a pro. Do the hard question first.",
        Virgo: "Small improvements = big results. Fix one weak point.",
        Libra: "Balance: 25 minutes focus, 5 minutes rest. Repeat.",
        Scorpio: "Deep focus mode. Ignore noise, lock in your goal.",
        Sagittarius: "Think big, execute small. Finish one chapter today.",
        Capricorn: "Discipline is your superpower. Keep going—quietly.",
        Aquarius: "Try a new method: active recall + short notes.",
        Pisces: "Calm mind, sharp brain. Breathe, then begin.",
        "—": "Set your birth date to see your calm study vibe."
      };
      const t = timeStr ? ` Birth time saved: ${timeStr}.` : "";
      return (base[sign] || base["—"]) + t;
    }

    function loadAstro() {
      const bd = localStorage.getItem("birthDate") || "";
      const bt = localStorage.getItem("birthTime") || "";
      birthDate.value = bd;
      birthTime.value = bt;

      if (bd) {
        const [y, m, d] = bd.split("-").map(n => parseInt(n, 10));
        const sign = getZodiac(m, d);
        zodiacEl.textContent = "Zodiac: " + sign;
        horoscopeText.textContent = calmMessage(sign, bt);
      } else {
        zodiacEl.textContent = "Zodiac: —";
        horoscopeText.textContent = "Add your birth date to see your sign and a calm “study vibe” message.";
      }
    }

    saveAstro.addEventListener("click", () => {
      if (!birthDate.value) {
        alert("Please choose your birth date first.");
        return;
      }
      localStorage.setItem("birthDate", birthDate.value);
      localStorage.setItem("birthTime", birthTime.value || "");
      loadAstro();
    });

    clearAstro.addEventListener("click", () => {
      localStorage.removeItem("birthDate");
      localStorage.removeItem("birthTime");
      birthDate.value = "";
      birthTime.value = "";
      loadAstro();
    });

    loadAstro();

    // ---------- Meteor Shower Intro ----------
    const overlay = document.getElementById("overlay");
    const sky = document.getElementById("sky");

    function spawnMeteor() {
      const m = document.createElement("div");
      m.className = "meteor";
      // random start position
      const top = Math.random() * 60 - 10; // -10% to 50%
      const left = 80 + Math.random() * 40; // 80% to 120%
      m.style.top = top + "%";
      m.style.left = left + "%";
      m.style.animationDuration = (1.2 + Math.random() * 1.2).toFixed(2) + "s";
      m.style.opacity = (0.6 + Math.random() * 0.4).toFixed(2);
      sky.appendChild(m);
      setTimeout(() => m.remove(), 2500);
    }

    // burst of meteors on load
    let bursts = 0;
    const burstInterval = setInterval(() => {
      for (let i = 0; i < 3; i++) spawnMeteor();
      bursts++;
      if (bursts >= 8) clearInterval(burstInterval);
    }, 280);

    // fade out overlay after a few seconds
    setTimeout(() => overlay.classList.add("hidden"), 4200);
    setTimeout(() => overlay.remove(), 5600);
  </script>
</body>
</html>
