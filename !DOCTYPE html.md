<!DOCTYPE html>  
  
<html lang="ja">  
<head>  
<meta charset="UTF-8">  
<title>Clock</title>  
<style>  
  * { margin: 0; padding: 0; box-sizing: border-box; }  
  
html, body {  
width: 100%;  
height: 100%;  
overflow: hidden;  
background: #FFFFFF;  
font-family: ‘Amazon Ember’, ‘Helvetica Neue’, Arial, sans-serif;  
color: #131A22;  
-webkit-font-smoothing: antialiased;  
cursor: default;  
}  
  
.container {  
width: 100vw;  
height: 100vh;  
display: flex;  
flex-direction: column;  
justify-content: center;  
align-items: center;  
position: relative;  
}  
  
/* Top bar - navy background, white text only here */  
.top-bar {  
position: absolute;  
top: 0;  
left: 0;  
right: 0;  
height: 56px;  
background: #131A22;  
display: flex;  
align-items: center;  
padding: 0 32px;  
}  
  
.logo {  
font-size: 22px;  
font-weight: 700;  
letter-spacing: -0.5px;  
color: #FFFFFF;  
position: relative;  
padding-bottom: 4px;  
}  
  
.logo::after {  
content: ‘’;  
position: absolute;  
bottom: 0;  
left: 6px;  
right: 12px;  
height: 8px;  
border-bottom: 2.5px solid #FF9900;  
border-radius: 0 0 50% 50% / 0 0 100% 100%;  
transform: scaleY(0.6);  
}  
  
.top-bar-meta {  
margin-left: auto;  
font-size: 12px;  
color: #FFFFFF;  
letter-spacing: 1.5px;  
text-transform: uppercase;  
font-weight: 500;  
opacity: 0.9;  
}  
  
/* Main display - white background, navy + orange */  
.clock-wrapper {  
text-align: center;  
position: relative;  
z-index: 1;  
}  
  
.timezone-label {  
font-size: 12px;  
letter-spacing: 4px;  
color: #131A22;  
text-transform: uppercase;  
margin-bottom: 24px;  
font-weight: 700;  
opacity: 0.6;  
}  
  
.time {  
font-size: 180px;  
font-weight: 600;  
letter-spacing: -4px;  
line-height: 1;  
color: #131A22;  
font-variant-numeric: tabular-nums;  
display: flex;  
justify-content: center;  
align-items: baseline;  
}  
  
.time .colon {  
color: #131A22;  
margin: 0 8px;  
font-weight: 500;  
}  
  
.date-row {  
display: flex;  
align-items: center;  
justify-content: center;  
gap: 24px;  
margin-top: 32px;  
font-size: 20px;  
color: #131A22;  
font-weight: 600;  
letter-spacing: 1px;  
}  
  
.date-row .divider {  
width: 5px;  
height: 5px;  
background: #131A22;  
border-radius: 50%;  
opacity: 0.5;  
}  
  
.weekday {  
color: #131A22;  
font-weight: 700;  
}  
  
/* Bottom bar - navy background, white text */  
.bottom-bar {  
position: absolute;  
bottom: 0;  
left: 0;  
right: 0;  
height: 48px;  
background: #131A22;  
display: flex;  
align-items: center;  
justify-content: space-between;  
padding: 0 32px;  
font-size: 11px;  
color: #FFFFFF;  
letter-spacing: 1.5px;  
text-transform: uppercase;  
font-weight: 500;  
}  
  
.status {  
display: flex;  
align-items: center;  
gap: 8px;  
}  
  
.status-dot {  
width: 6px;  
height: 6px;  
background: #FF9900;  
border-radius: 50%;  
}  
  
.progress-section {  
display: flex;  
align-items: center;  
gap: 12px;  
}  
  
.progress-bar {  
width: 200px;  
height: 2px;  
background: rgba(255, 255, 255, 0.2);  
position: relative;  
overflow: hidden;  
}  
  
.progress-fill {  
position: absolute;  
top: 0;  
left: 0;  
height: 100%;  
background: #FF9900;  
transition: width 1s linear;  
}  
  
/* Subtle ambient glow on white */  
.ambient {  
position: absolute;  
top: 50%;  
left: 50%;  
transform: translate(-50%, -50%);  
width: 900px;  
height: 900px;  
background: radial-gradient(circle, rgba(255, 153, 0, 0.06) 0%, transparent 65%);  
pointer-events: none;  
z-index: 0;  
}  
  
@media (max-width: 900px) {  
.time { font-size: 110px; letter-spacing: -3px; }  
.seconds { font-size: 44px; }  
.date-row { font-size: 14px; gap: 16px; }  
.progress-bar { width: 120px; }  
}  
  
@media (max-width: 500px) {  
.time { font-size: 72px; letter-spacing: -2px; }  
.seconds { font-size: 28px; }  
.top-bar { padding: 0 16px; }  
.bottom-bar { padding: 0 16px; }  
.top-bar-meta { display: none; }  
}  
</style>  
  
</head>  
<body>  
<div class="container">  
  <div class="ambient"></div>  
  
  <div class="top-bar">  
    <div class="logo">amazon</div>  
    <div class="top-bar-meta" id="meta">JST · TOKYO</div>  
  </div>  
  
  <div class="clock-wrapper">  
    <div class="timezone-label">Japan Standard Time</div>  
    <div class="time">  
      <span id="hours">00</span><span class="colon">:</span><span id="minutes">00</span><span class="colon">:</span><span id="seconds">00</span>  
    </div>  
    <div class="date-row">  
      <span id="date">2026年5月5日</span>  
      <span class="divider"></span>  
      <span class="weekday" id="weekday">火曜日</span>  
      <span class="divider"></span>  
      <span id="week">Week 19</span>  
    </div>  
  </div>  
  
  <div class="bottom-bar">  
    <div class="status">  
      <span class="status-dot"></span>  
      <span>SYNCED</span>  
    </div>  
    <div class="progress-section">  
      <span id="progress-label">DAY PROGRESS</span>  
      <div class="progress-bar">  
        <div class="progress-fill" id="progress"></div>  
      </div>  
      <span id="progress-pct">0%</span>  
    </div>  
  </div>  
</div>  
  
<script>  
  const weekdays = ['日曜日', '月曜日', '火曜日', '水曜日', '木曜日', '金曜日', '土曜日'];  
    
  function getJSTDate() {  
    const now = new Date();  
    const utc = now.getTime() + (now.getTimezoneOffset() * 60000);  
    return new Date(utc + (9 * 3600000));  
  }  
    
  function getWeekNumber(date) {  
    const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()));  
    const dayNum = d.getUTCDay() || 7;  
    d.setUTCDate(d.getUTCDate() + 4 - dayNum);  
    const yearStart = new Date(Date.UTC(d.getUTCFullYear(), 0, 1));  
    return Math.ceil((((d - yearStart) / 86400000) + 1) / 7);  
  }  
    
  function pad(n) {  
    return n.toString().padStart(2, '0');  
  }  
    
  function update() {  
    const d = getJSTDate();  
    const h = d.getHours();  
    const m = d.getMinutes();  
    const s = d.getSeconds();  
      
    document.getElementById('hours').textContent = pad(h);  
    document.getElementById('minutes').textContent = pad(m);  
    document.getElementById('seconds').textContent = pad(s);  
      
    const dateStr = `${d.getFullYear()}年${d.getMonth() + 1}月${d.getDate()}日`;  
    document.getElementById('date').textContent = dateStr;  
    document.getElementById('weekday').textContent = weekdays[d.getDay()];  
    document.getElementById('week').textContent = `Week ${getWeekNumber(d)}`;  
      
    const totalSecondsInDay = 24 * 3600;  
    const elapsedSeconds = h * 3600 + m * 60 + s;  
    const pct = (elapsedSeconds / totalSecondsInDay) * 100;  
    document.getElementById('progress').style.width = pct + '%';  
    document.getElementById('progress-pct').textContent = pct.toFixed(1) + '%';  
  }  
    
  update();  
  setInterval(update, 1000);  
</script>  
  
</body>  
</html>  
