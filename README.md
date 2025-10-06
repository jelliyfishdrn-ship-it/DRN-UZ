<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>106 Legenda</title>
<style>
/* 🌌 Umumiy dizayn */
body {
  margin: 0;
  padding: 0;
  font-family: 'Poppins', sans-serif;
  background: linear-gradient(135deg, #0c0c0c, #1a1a1a, #0f0f0f);
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

h1, h2, h3 {
  text-align: center;
  color: #9b5fff;
  text-shadow: 0 0 10px #7e2fff;
}

.screen {
  display: none;
  background: rgba(20, 0, 35, 0.85);
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 0 25px #7e2fff;
  width: 90%;
  max-width: 500px;
}

.screen.active {
  display: block;
}

.hidden { display: none; }

input, select, textarea, button {
  width: 100%;
  margin: 8px 0;
  padding: 10px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  box-sizing: border-box;
}

input, textarea, select {
  background: #1b1b1b;
  color: #fff;
  border: 1px solid #7e2fff;
}

button {
  background: linear-gradient(90deg, #7e2fff, #9b5fff);
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  box-shadow: 0 0 15px #a76cff;
  transform: scale(1.03);
}

/* 🔹 Admin paneli tugmalari */
.admin-controls {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  margin: 15px 0;
}

.admin-controls button {
  flex: 1 1 45%;
  background: linear-gradient(90deg, #6200ea, #b54bff);
}

.admin-controls button.active {
  box-shadow: 0 0 20px #fff;
  transform: scale(1.05);
}

.admin-section {
  background: rgba(10, 0, 25, 0.85);
  padding: 15px;
  border-radius: 12px;
  box-shadow: 0 0 15px #7a35d3;
  margin-top: 10px;
}

#profile-pic {
  display: block;
  margin: 0 auto;
  border-radius: 50%;
  border: 3px solid #b76aff;
  box-shadow: 0 0 15px #a76cff;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#video-list iframe, video {
  width: 100%;
  margin-top: 10px;
  border-radius: 10px;
}

#pdf-list iframe {
  width: 100%;
  height: 400px;
  border: 1px solid #b76aff;
  border-radius: 8px;
}

#test-list button {
  margin: 5px 2px;
  width: 48%;
  background: #2e005e;
  border: 1px solid #a355ff;
}

#test-list button:hover {
  background: #6200ea;
}

@media (max-width: 600px) {
  .screen {
    width: 95%;
    padding: 15px;
  }
  button, input, textarea {
    font-size: 14px;
  }
  h1, h2, h3 {
    font-size: 18px;
  }
}
</style>
</head>
<body>

<!-- 🔹 Kirish -->
<div id="login-screen" class="screen active">
  <h1>106 Legenda</h1>
  <input type="text" id="userEmail" placeholder="Email yoki telefon">
  <input type="password" id="userPassword" placeholder="Parol">
  <button onclick="userLogin()">Kirish</button>
  <button onclick="showRegister()">Ro‘yxatdan o‘tish</button>
  <p style="margin-top:20px;">Adminmisiz? <a href="#" onclick="showAdminLogin()">Admin kirish</a></p>
</div>

<!-- 🔹 Ro‘yxatdan o‘tish -->
<div id="register-screen" class="screen hidden">
  <h2>Ro‘yxatdan o‘tish</h2>
  <input type="text" id="newUserEmail" placeholder="Email yoki telefon">
  <input type="password" id="newUserPassword" placeholder="Parol">
  <button onclick="registerUser()">Ro‘yxatdan o‘tish</button>
  <button onclick="backToLogin()">Ortga</button>
</div>

<!-- 🔹 Admin login -->
<div id="admin-login" class="screen hidden">
  <h2>Admin kirish</h2>
  <input type="text" id="adminName" placeholder="Login (jelliyfish.drn)">
  <input type="password" id="adminPass" placeholder="Parol (meduza.1324)">
  <button onclick="adminLogin()">Kirish</button>
  <button onclick="backToLogin()">Ortga</button>
</div>

<!-- 🔹 Foydalanuvchi paneli -->
<div id="user-panel" class="screen hidden">
  <header>
    <h2>106 Legenda — Foydalanuvchi paneli</h2>
    <button onclick="logout()">Chiqish</button>
  </header>
  <section id="videos-section">
    <h3>🎬 Videolar</h3>
    <div id="video-list"></div>
  </section>
  <section id="pdf-section">
    <h3>📚 Manga / Manhua (PDF)</h3>
    <div id="pdf-list"></div>
  </section>
  <section id="test-section">
    <h3>🧩 Testlar</h3>
    <div id="test-list"></div>
  </section>
  <section id="profile-section">
    <h3>👤 Profil</h3>
    <img id="profile-pic" src="" alt="Profil rasmi" width="100">
    <input type="file" id="upload-pic" accept="image/*" onchange="uploadProfilePic(event)">
  </section>
</div>

<!-- 🔹 Admin panel -->
<div id="admin-panel" class="screen hidden">
  <header>
    <h2>106 Legenda — Admin panel</h2>
    <button onclick="logout()">Chiqish</button>
  </header>

  <div class="admin-controls">
    <button onclick="showAdminSection('video')">🎬 Video qo‘shish</button>
    <button onclick="showAdminSection('pdf')">📚 PDF yuklash</button>
    <button onclick="showAdminSection('ad')">📰 Reklama</button>
    <button onclick="showAdminSection('test')">🧩 Testlar</button>
    <button onclick="showAdminSection('subs')">👥 Obunachilar</button>
  </div>

  <section id="admin-video" class="admin-section hidden">
    <h3>🎬 Video joylash</h3>
    <input type="text" id="youtube-link" placeholder="YouTube havola">
    <input type="file" id="video-file" accept="video/*">
    <button onclick="addVideo()">Saqlash</button>
  </section>

  <section id="admin-pdf" class="admin-section hidden">
    <h3>📚 PDF yuklash</h3>
    <input type="file" id="pdf-file" accept="application/pdf">
    <button onclick="addPDF()">Saqlash</button>
  </section>

  <section id="admin-ad" class="admin-section hidden">
    <h3>📰 Reklama joylash</h3>
    <textarea id="ad-text" placeholder="Reklama matni..."></textarea>
    <button onclick="addAd()">Saqlash</button>
  </section>

  <section id="admin-test" class="admin-section hidden">
    <h3>🧩 Test yaratish</h3>
    <input type="text" id="test-question" placeholder="Savol matni">
    <input type="text" id="test-a" placeholder="A javob">
    <input type="text" id="test-b" placeholder="B javob">
    <input type="text" id="test-c" placeholder="C javob">
    <input type="text" id="test-d" placeholder="D javob">
    <select id="test-correct">
      <option value="A">A</option>
      <option value="B">B</option>
      <option value="C">C</option>
      <option value="D">D</option>
    </select>
    <button onclick="addTest()">Saqlash</button>
  </section>

  <section id="admin-subs" class="admin-section hidden">
    <h3>👥 Obunachilar ro‘yxati</h3>
    <div id="subscribers-list"></div>
  </section>
</div>

<script>
// 🌌 JavaScript logikasi
let users = JSON.parse(localStorage.getItem("users") || "[]");
let videos = JSON.parse(localStorage.getItem("videos") || "[]");
let pdfs = JSON.parse(localStorage.getItem("pdfs") || "[]");
let ads = JSON.parse(localStorage.getItem("ads") || "[]");
let tests = JSON.parse(localStorage.getItem("tests") || "[]");
let currentUser = JSON.parse(localStorage.getItem("currentUser") || "null");
const screens = document.querySelectorAll(".screen");

function showScreen(id){
  screens.forEach(s=>{ s.classList.remove("active"); s.classList.add("hidden"); });
  const screen=document.getElementById(id);
  screen.classList.remove("hidden");
  screen.classList.add("active");
}

window.onload = ()=>{
  if(currentUser && currentUser.type==="admin") showScreen("admin-panel");
  else if(currentUser && currentUser.type==="user") showScreen("user-panel");
  else showScreen("login-screen");
};

function adminLogin(){
  const login=document.getElementById("adminName").value.trim();
  const pass=document.getElementById("adminPass").value.trim();
  if(login==="jelliyfish.drn" && pass==="meduza.1324"){
    currentUser={type:"admin", name:"Admin"};
    localStorage.setItem("currentUser", JSON.stringify(currentUser));
    showScreen("admin-panel");
    renderAdmin();
  }else alert("Login yoki parol noto‘g‘ri!");
}

function userLogin(){
  const email=document.getElementById("userEmail").value.trim();
  const pass=document.getElementById("userPassword").value.trim();
  const user=users.find(u=>u.email===email && u.pass===pass);
  if(user){
    currentUser={type:"user", email};
    localStorage.setItem("currentUser", JSON.stringify(currentUser));
    showScreen("user-panel");
    renderUser();
  }else alert("Foydalanuvchi topilmadi!");
}

function registerUser(){
  const email=document.getElementById("newUserEmail").value.trim();
  const pass=document.getElementById("newUserPassword").value.trim();
  if(users.find(u=>u.email===email)){ alert("Bu foydalanuvchi allaqachon mavjud!"); return; }
  users.push({email,pass});
  localStorage.setItem("users", JSON.stringify(users));
  alert("Ro‘yxatdan o‘tish muvaffaqiyatli!");
  showScreen("login-screen");
}

function logout(){ localStorage.removeItem("currentUser"); currentUser=null; showScreen("login-screen"); }

function showRegister(){ showScreen("register-screen"); }
function backToLogin(){ showScreen("login-screen"); }
function showAdminLogin(){ showScreen("admin-login"); }

function addVideo(){
  const yt=document.getElementById("youtube-link").value.trim();
  const file=document.getElementById("video-file").files[0];
  if(yt) videos.push({type:"youtube", src:yt});
  else if(file) videos.push({type:"file", src:URL.createObjectURL(file)});
  else{ alert("Video tanlang yoki havola kiriting!"); return; }
  localStorage.setItem("videos", JSON.stringify(videos));
  alert("Video saqlandi!");
  renderAdmin(); renderUser();
}

function addPDF(){
  const file=document.getElementById("pdf-file").files[0];
  if(!file) return alert("PDF tanlang!");
  pdfs.push({src:URL.createObjectURL(file), name:file.name});
  localStorage.setItem("pdfs", JSON.stringify(pdfs));
  alert("PDF saqlandi!"); renderAdmin(); renderUser();
}

function addAd(){
  const text=document.getElementById("ad-text").value.trim();
  if(!text) return alert("Reklama matnini kiriting!");
  ads.push({text}); localStorage.setItem("ads", JSON.stringify(ads));
  alert("Reklama saqlandi!"); renderAdmin(); renderUser();
}

function addTest(){
  const q=document.getElementById("test-question").value;
  const a=document.getElementById("test-a").value;
  const b=document.getElementById("test-b").value;
  const c=document.getElementById("test-c").value;
  const d=document.getElementById("test-d").value;
  const correct=document.getElementById("test-correct").value;
  tests.push({q,a,b,c,d,correct});
  localStorage.setItem("tests", JSON.stringify(tests));
  alert("Test saqlandi!"); renderAdmin(); renderUser();
}

function uploadProfilePic(e){
  const file=e.target.files[0]; if(!file) return;
  const reader=new FileReader();
  reader.onload=function(evt){ document.getElementById("profile-pic").src=evt.target.result; localStorage.setItem("profilePic", evt.target.result); };
  reader.readAsDataURL(file);
}

function renderAdmin(){
  document.getElementById("subscribers-list").innerHTML=users.map(u=>`<p>${u.email}</p>`).join("")||"Foydalanuvchi yo‘q.";
}

function renderUser(){
  document.getElementById("video-list").innerHTML=videos.map(v=>v.type==="youtube"?`<iframe src="${v.src.replace("watch?v=","embed/")}" allowfullscreen></iframe>`:`<video controls src="${v.src}"></video>`).join("")||"Video yo‘q.";
  document.getElementById("pdf-list").innerHTML=pdfs.map(p=>`<iframe src="${p.src}"></iframe><p>${p.name}</p>`).join("")||"PDF yo‘q.";
  document.getElementById("test-list").innerHTML=tests.map((t,i)=>`<div class='test'><p>${i+1}. ${t.q}</p>${['A','B','C','D'].map(v=>`<button onclick="checkAnswer(${i},'${v}')">${v}) ${t[v.toLowerCase()]}</button>`).join('')}</div>`).join("")||"Test yo‘q.";
  const savedPic=localStorage.getItem("profilePic"); if(savedPic) document.getElementById("profile-pic").src=savedPic;
}

function checkAnswer(index, ans){
  const correct=tests[index].correct;
  if(ans===correct) alert("✅ To‘g‘ri javob!");
  else alert("❌ Noto‘g‘ri, to‘g‘ri javob: "+correct);
}

function showAdminSection(id){
  document.querySelectorAll(".admin-section").forEach(s=>s.classList.add("hidden"));
  document.getElementById("admin-"+id).classList.remove("hidden");
  document.querySelectorAll(".admin-controls button").forEach(b=>b.classList.remove("active"));
  document.querySelector(`.admin-controls button[onclick="showAdminSection('${id}')"]`).classList.add("active");
}
</script>
</body>
</html>