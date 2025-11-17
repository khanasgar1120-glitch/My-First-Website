<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Apps Home — Login</title>

  <style>
    * { box-sizing: border-box; margin:0; padding:0; font-family: 'Poppins', sans-serif; }
    html,body { height:100%; }

    body {
      height:100vh; display:flex; align-items:center; justify-content:center;
      background:#f0f7ff; color:#222; padding-top:90px;
      transition: background-color 1s ease;
    }

    /* HEADER CLOCK */
    header.topbar {
      position: fixed;
      top:10px; left:10px; right:10px;
      display:flex; justify-content:flex-end;
      align-items:center;
      padding:10px 16px;
      background: rgba(255,255,255,0.85);
      border-radius:12px;
      backdrop-filter: blur(6px);
      box-shadow: 0 8px 24px rgba(0,0,0,0.12);
      z-index:100;
    }

    .clock-right { display:flex; align-items:center; gap:6px; }

    .time-box {
      min-width:52px; height:42px;
      display:flex; align-items:center; justify-content:center;
      padding:6px 12px;
      border-radius:8px; background:#ffffff;
      font-weight:700; font-size:16px;
      transition: background-color .8s ease;
    }

    /* LOGIN FORM */
    .card {
      width:380px; max-width:94%; padding:36px;
      border-radius:14px;
      background:#ffffffd9;
      backdrop-filter: blur(10px);
      box-shadow: 0 10px 40px rgba(0,0,0,0.14);
      text-align:center;
      transition: background-color 1s ease;
    }

    .title { font-size:20px; margin-bottom:14px; color:#111; }

    input {
      width:100%; padding:12px 14px; border-radius:8px; border:0;
      background:#fff; font-size:15px;
      box-shadow: 0 6px 14px rgba(0,0,0,0.06);
      margin:10px 0;
    }

    .show-pass {
      position:absolute; right:12px; top:50%; transform:translateY(-50%);
      cursor:pointer; user-select:none;
    }

    .btn {
      width:100%; padding:12px; margin-top:12px;
      border-radius:8px; border:0; cursor:pointer;
      background:linear-gradient(135deg,#00bcd4,#2196f3);
      color:#fff; font-weight:700; font-size:15px;
    }

    /* HOME PAGE */
    .home {
      display:none; width:760px; max-width:96%; padding:28px;
      border-radius:12px; background:#fff;
      box-shadow:0 12px 36px rgba(0,0,0,0.08); text-align:center;
    }

    .apps-grid {
      display:grid; grid-template-columns: repeat(3,1fr);
      gap:18px; margin-top:20px;
    }

    .app-card {
      width:120px; height:120px; background:#fff;
      border-radius:16px; padding:10px;
      display:flex; flex-direction:column;
      align-items:center; justify-content:center;
      font-weight:600; text-decoration:none; color:#000;
      box-shadow:0 6px 18px rgba(0,0,0,0.08);
      transition:.15s;
    }

    .app-card img {
      width:48px; height:48px; margin-bottom:8px;
    }

    .app-card:hover { transform:translateY(-6px); }

    .logout {
      margin-top:18px; padding:10px; border-radius:9px;
      background:linear-gradient(135deg,#f44336,#e91e63);
      border:0; color:#fff; font-weight:700; cursor:pointer;
    }
  </style>
</head>
<body>

<header class="topbar">
  <div class="clock-right">
    <div class="time-box" id="hBox">--</div>
    <div class="time-box" id="mBox">--</div>
    <div class="time-box" id="sBox">--</div>
    <div class="time-box" id="apBox">--</div>
  </div>
</header>

<!-- LOGIN -->
<div class="card" id="loginBox">
  <div class="title">Please ye form login karen</div>

  <input id="username" type="text" placeholder="Username" />
  <div class="input-box" style="position:relative;">
    <input id="password" type="password" placeholder="Password" />
    <span class="show-pass" id="showPass">👁️</span>
  </div>

  <button id="loginBtn" class="btn">Login</button>
</div>

<!-- HOME PAGE -->
<div class="home" id="homePage">
  <h1 id="welcomeText">Welcome!</h1>

  <div class="apps-grid">

    <a class="app-card" href="https://www.youtube.com/" target="_blank">
      <img src="https://cdn-icons-png.flaticon.com/512/1384/1384060.png">
      YouTube
    </a>

    <a class="app-card" href="https://web.whatsapp.com/" target="_blank">
      <img src="https://cdn-icons-png.flaticon.com/512/3670/3670051.png">
      WhatsApp
    </a>

    <a class="app-card" href="https://chat.openai.com/" target="_blank">
      <img src="https://cdn-icons-png.flaticon.com/512/11660/11660783.png">
      ChatGPT
    </a>

    <a class="app-card" href="https://play.google.com/store" target="_blank">
      <img src="https://cdn-icons-png.flaticon.com/512/300/300218.png">
      Play Store
    </a>

    <a class="app-card" href="https://www.instagram.com/" target="_blank">
      <img src="https://cdn-icons-png.flaticon.com/512/2111/2111463.png">
      Instagram
    </a>

  </div>

  <button id="logoutBtn" class="logout">Log Out</button>
</div>

<script>
function lightColor() {
  const r = Math.floor(180 + Math.random() * 60);
  const g = Math.floor(180 + Math.random() * 60);
  const b = Math.floor(180 + Math.random() * 60);
  return `rgb(${r},${g},${b})`;
}

function uniqueColor(prev) {
  let c = lightColor();
  while (c === prev) c = lightColor();
  return c;
}

function getIST() {
  const now = new Date();
  const utc = now.getTime() + now.getTimezoneOffset()*60000;
  return new Date(utc + 5.5*3600000);
}

function updateClock() {
  const t = getIST();
  let h = t.getHours(), m = t.getMinutes(), s = t.getSeconds();
  let ap = h >= 12 ? "PM" : "AM";
  h = h % 12 || 12;
  hBox.textContent = String(h).padStart(2,"0");
  mBox.textContent = String(m).padStart(2,"0");
  sBox.textContent = String(s).padStart(2,"0");
  apBox.textContent = ap;
}

setInterval(()=>{
  hBox.style.backgroundColor = lightColor();
  mBox.style.backgroundColor = lightColor();
  sBox.style.backgroundColor = lightColor();
  apBox.style.backgroundColor = lightColor();
},3000);

setInterval(updateClock,1000);
updateClock();

let lastBody = "";
let lastCard = "";

setInterval(() => {
  const bodyC = uniqueColor(lastBody);
  const cardC = uniqueColor(lastCard);
  document.body.style.backgroundColor = bodyC;
  document.getElementById("loginBox").style.backgroundColor = cardC;
  lastBody = bodyC;
  lastCard = cardC;
}, 3000);

showPass.onclick = () => {
  password.type = password.type === "password" ? "text" : "password";
};

loginBtn.onclick = ()=>{
  if(!username.value || !password.value){
    alert("Please enter username and password");
    return;
  }
  welcomeText.textContent = "Welcome, " + username.value + "!";
  loginBox.style.display="none";
  homePage.style.display="block";
};

logoutBtn.onclick = ()=>{
  homePage.style.display="none";
  loginBox.style.display="block";
  username.value="";
  password.value="";
};
</script>

</body>
</html>
