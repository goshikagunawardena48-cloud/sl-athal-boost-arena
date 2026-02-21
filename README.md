<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SL Athal Boost | Fan Gaming Platform</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;font-family:'Poppins',sans-serif}
body{margin:0;background:radial-gradient(circle at top,#0f2027,#000);color:white;min-height:100vh;overflow-y:auto;padding-bottom: 60px;}
.hidden{display:none}
header{padding:15px;text-align:center;font-size:26px;font-weight:700;background:rgba(0,0,0,.5);letter-spacing:1px}
.container{padding:20px;max-width:1100px;margin:auto;text-align:center}
.card{background:rgba(255,255,255,.08);padding:25px;border-radius:20px;box-shadow:0 0 30px rgba(0,0,0,.6);margin-bottom:20px}
input,button{padding:12px;border:none;border-radius:12px;font-size:15px;margin:6px;width:100%}
input{background:#fff;color:#000}
button{background:linear-gradient(135deg,#ff512f,#dd2476);color:white;font-weight:600;cursor:pointer;transition:.3s}
button:hover{transform:scale(1.05)}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px}
.widget{text-align:center;background:rgba(255,255,255,.07);padding:15px;border-radius:16px}
.rank{font-size:22px;font-weight:700;color:#00ffcc}
footer{text-align:center;padding:10px;font-size:12px;opacity:.7;position:fixed;bottom:0;width:100%;background:rgba(0,0,0,.8);z-index:100}
.loader{width:70px;height:70px;border:7px solid rgba(255,255,255,.2);border-top:7px solid #fff;border-radius:50%;animation:spin 1s linear infinite;margin:auto}
@keyframes spin{to{transform:rotate(360deg)}}
.logo{font-size:48px;font-weight:800;background:linear-gradient(90deg,#ff512f,#dd2476,#24c6dc);-webkit-background-clip:text;color:transparent;animation:glow 2s infinite}
@keyframes glow{0%,100%{text-shadow:0 0 10px #ff512f}50%{text-shadow:0 0 25px #24c6dc}}
.fadeIn{animation:fade .6s}
@keyframes fade{from{opacity:0;transform:scale(.9)}to{opacity:1;transform:scale(1)}}
</style>
</head>
<body>

<header>SL ආතල් Boost 🔥 | Fan Gaming Community</header>

<div id="loading" class="container fadeIn">
  <div class="loader"></div>
  <p>Loading Platform...</p>
</div>

<div id="auth" class="container hidden fadeIn">
  <div class="card">
    <div class="logo">SL ආතල් Boost</div>
    <p>Welcome to Sri Lanka #1 Fan Gaming Platform</p>
    <input id="username" placeholder="@username">
    <input id="email" placeholder="example@example.com">
    <input id="password" type="password" placeholder="Strong Password">
    <button onclick="login(event)">Login</button>
    <button onclick="signup(event)">Sign Up</button>
  </div>
</div>

<div id="welcome" class="container hidden fadeIn">
  <div class="card">
    <div class="logo">SL ආතල් Boost</div>
    <h2 id="welcomeText"></h2>
    <p>You are now part of the official gaming community 🔥</p>
    <button onclick="enterDashboard(event)">ENTER GAMING ZONE</button>
  </div>
</div>

<div id="dashboard" class="container hidden fadeIn">
  <div class="card">
    <h2>🎮 Player Dashboard</h2>
    <p>Points: <span id="pointsDisplay">0</span></p>
    <p class="rank">Rank: <span id="rankDisplay">Beginner</span></p>
  </div>

  <div class="grid">
    <div class="widget">
      <h3>🎯 Reaction Game</h3>
      <p id="reaction">Wait...</p>
      <button onclick="startReaction(event)">Start</button>
    </div>

    <div class="widget">
      <h3>🧠 Quiz</h3>
      <p>Subscribers?</p>
      <button onclick="quiz('3671', event)">3671</button>
      <button onclick="quiz('5000', event)">5000</button>
    </div>

    <div class="widget">
      <h3>🏁 Daily Challenge</h3>
      <p id="daily">0 / 100</p>
      <button onclick="dailyClick(event)">CLICK</button>
    </div>

    <div class="widget">
      <h3>🏆 Leaderboard</h3>
      <div id="leaderboard">Coming Soon...</div>
    </div>
  </div>

  <button style="margin-top:20px;background:#444" onclick="logout(event)">Logout</button>
</div>

<footer>© 2026 SL ATHAL BOOST | Official Fan Gaming Platform</footer>

<script>
// Cache DOM Elements
const loading = document.getElementById('loading');
const auth = document.getElementById('auth');
const welcome = document.getElementById('welcome');
const dashboard = document.getElementById('dashboard');
const welcomeText = document.getElementById('welcomeText');
const pointsEl = document.getElementById('pointsDisplay');
const rankEl = document.getElementById('rankDisplay');
const dailyEl = document.getElementById('daily');
const reactionEl = document.getElementById('reaction');

let points = 0, reactionStart = 0, daily = 0, currentUser = '';

// Fake Loader
setTimeout(() => {
  loading.classList.add('hidden');
  auth.classList.remove('hidden');
}, 1500);

function signup(e) {
  if(e) e.stopPropagation();
  const u = document.getElementById('username').value.trim();
  const p = document.getElementById('password').value.trim();
  const em = document.getElementById('email').value.trim();

  if(!u || !p || !em) return alert('Fill all fields');
  if(!/^@\w{3,}$/.test(u)) return alert('Username must start with @');
  if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(em)) return alert('Invalid email');
  if(p.length < 8) return alert('Password must be 8+ characters');

  localStorage.setItem('user', JSON.stringify({u, p, em, points: 0}));
  alert('Signup successful. Please login!');
}

function login(e) {
  if(e) e.stopPropagation();
  const u = document.getElementById('username').value.trim();
  const p = document.getElementById('password').value.trim();
  let data = JSON.parse(localStorage.getItem('user') || '{}');

  if(data.u === u && data.p === p) {
    currentUser = u;
    points = data.points || 0;
    welcomeText.innerText = 'Welcome Back ' + u + ' 🔥';
    auth.classList.add('hidden');
    welcome.classList.remove('hidden');
  } else {
    alert('Invalid login or please sign up first');
  }
}

function enterDashboard(e) {
  if(e) e.stopPropagation();
  welcome.classList.add('hidden');
  dashboard.classList.remove('hidden');
  updateUI();
}

function logout(e) {
  if(e) e.stopPropagation();
  location.reload();
}

function updateUI() {
  pointsEl.innerText = Math.floor(points);
  rankEl.innerText = points < 100 ? 'Beginner' : points < 500 ? 'Pro Fan' : 'Legend';
}

function startReaction(e) {
  e.stopPropagation(); // Prevents instant clicking
  reactionEl.innerText = 'Get Ready...';
  setTimeout(() => {
    reactionStart = Date.now();
    reactionEl.innerText = 'CLICK NOW!';
  }, 1000 + Math.random() * 2000);
}

// Global Click for Reaction Game
document.body.onclick = () => {
  if(reactionStart) {
    let t = Date.now() - reactionStart;
    reactionEl.innerText = t + ' ms';
    reactionStart = 0;
    addPoints(Math.max(0, 1000 - t));
  }
}

function quiz(a, e) {
  e.stopPropagation();
  if(a === '3671') {
    alert('Correct +200');
    addPoints(200);
  } else {
    alert('Wrong');
  }
}

function dailyClick(e) {
  e.stopPropagation();
  daily++;
  dailyEl.innerText = daily + ' / 100';
  if(daily === 100) {
    alert('🔥 Daily Challenge Completed! +10000 Points');
    addPoints(10000);
    daily = 0; // Reset for next time
  }
}

function addPoints(p) {
  points += p;
  updateUI();
  // Save progress
  let data = JSON.parse(localStorage.getItem('user') || '{}');
  if(data.u) {
    data.points = points;
    localStorage.setItem('user', JSON.stringify(data));
  }
}
</script>
</body>
</html>
