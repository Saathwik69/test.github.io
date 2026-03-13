<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Open When 💌</title>
<link href="https://fonts.googleapis.com/css2?family=Patrick+Hand&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">

<style>
:root{
--pink:#ffd6e0;
--accent:#ff8fab;
--cream:#fff9fb;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{
font-family:'Quicksand',sans-serif;
background:linear-gradient(135deg,#ffe0ec,#fff0f5);
min-height:100vh;
display:flex;
align-items:center;
justify-content:center;
overflow-x:hidden;
cursor:none;
}
#lockscreen{
position:fixed;
top:0;left:0;width:100%;height:100%;
background:linear-gradient(135deg,#ffd6e0,#fff0f5);
display:flex;flex-direction:column;align-items:center;justify-content:center;
z-index:9999;font-family:'Patrick Hand',cursive;
}
#lockscreen button{
margin-top:20px;padding:12px 30px;border:none;border-radius:30px;background:#ff8fab;color:white;font-size:18px;cursor:pointer;
}
.paper{
background:var(--cream);padding:40px;border-radius:20px;box-shadow:0 20px 40px rgba(0,0,0,.2);width:90%;max-width:700px;text-align:center;position:relative;
}
.tape{
position:absolute;top:-12px;left:50%;transform:translateX(-50%);width:120px;height:25px;background:rgba(255,255,255,.7);border-radius:5px;
}
.sticker{
position:absolute;font-size:28px;animation:floatSticker 4s ease-in-out infinite;
}
.s1{top:-15px;right:30px;}
.s2{bottom:-15px;left:20px;}
@keyframes floatSticker{
0%,100%{transform:rotate(-5deg)}
50%{transform:rotate(5deg)}
}
.dark{background:black;color:white;}
.dark::before{
content:"";position:fixed;top:0;left:0;width:100%;height:100%;
background-image:radial-gradient(white 1px,transparent 1px);
background-size:40px 40px;opacity:.3;pointer-events:none;
}
.star{position:fixed;top:0;width:2px;height:80px;background:white;opacity:.7;transform:rotate(45deg);animation:shoot 2s linear;}
@keyframes shoot{
0%{transform:translateY(0) rotate(45deg)}
100%{transform:translateY(800px) translateX(300px) rotate(45deg)}
}
.heart{position:fixed;bottom:-10px;animation:float 8s linear infinite;}
@keyframes float{
0%{transform:translateY(0)}
100%{transform:translateY(-120vh)}
}
@keyframes fallBlossom{
0%{transform:translateY(0)}
100%{transform:translateY(110vh)}
}
.confetti{position:fixed;top:-10px;width:8px;height:8px;animation:fall 3s linear;}
@keyframes fall{
0%{transform:translateY(0)}
100%{transform:translateY(100vh) rotate(720deg)}
}
.cursor-heart{position:fixed;pointer-events:none;font-size:20px;transform:translate(-50%,-50%);}
.screen{display:none;}.active{display:block;}
.btn{background:var(--accent);color:white;border:none;padding:12px 28px;border-radius:40px;font-size:18px;cursor:pointer;margin-top:15px;}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:20px;margin-top:20px;}
.envelope{background:white;border-radius:15px;padding:25px;cursor:pointer;box-shadow:0 6px 12px rgba(0,0,0,.1);position:relative;transition:.3s;}
.envelope:hover{transform:translateY(-6px) scale(1.05);}
.envelope::after{content:"✉️";position:absolute;font-size:40px;top:10px;left:50%;transform:translateX(-50%);transition:.4s;}
.envelope:hover::after{transform:translate(-50%,-15px) rotate(-12deg);}
.modal{position:fixed;top:0;left:0;width:100%;height:100%;display:none;background:rgba(255,220,230,.8);align-items:center;justify-content:center;backdrop-filter:blur(6px);}
.modal-box{background:white;padding:30px;border-radius:20px;width:90%;max-width:520px;text-align:center;}
.gallery{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-top:10px;}
.gallery img{width:100%;border-radius:10px;}
.timeline{margin-top:15px;max-height:300px;overflow-y:auto;}
.moment{margin-bottom:20px;}
.moment img{width:100%;border-radius:12px;}
.close{margin-top:10px;background:var(--accent);color:white;border:none;padding:8px 20px;border-radius:20px;cursor:pointer;}
.music-btn,.dark-toggle{position:absolute;top:15px;background:white;border-radius:50%;width:40px;height:40px;display:flex;align-items:center;justify-content:center;cursor:pointer;}
.music-btn{left:15px;}
.dark-toggle{right:15px;}
</style>
</head>
<body>

<div id="lockscreen">
<h2>💌 A message for you</h2>
<p>tap to unlock</p>
<button onclick="unlock()">unlock</button>
</div>

<div class="paper">

<div class="tape"></div>
<div class="sticker s1">🌸</div>
<div class="sticker s2">💗</div>

<div class="music-btn" onclick="toggleMusic()">🎵</div>
<div class="dark-toggle" onclick="toggleDark()">🌙</div>

<audio id="music" loop>
<source src="user/music.mpeg" type="audio/mpeg">
</audio>

<div class="screen active" id="s1">
<h1>I made something for you 💌</h1>
<p id="typing"></p>
<button class="btn" onclick="next(2)">what?</button>
</div>

<div class="screen" id="s2">
<h1>Open When...</h1>
<div class="grid">
<div class="envelope" onclick="openModal('m1')">miss me</div>
<div class="envelope" onclick="openModal('m2')">you're sad</div>
<div class="envelope" onclick="openModal('gallery')">our memories</div>
<div class="envelope" onclick="openModal('timeline')">our story</div>
<div class="envelope" onclick="openModal('video')">video message</div>
<div class="envelope" onclick="openModal('reasons')">100 reasons</div>
<div class="envelope" onclick="openModal('game')">love notes</div>
<div class="envelope" onclick="openSecret()">secret</div>
</div>
</div>

</div>

<!-- Modals -->
<div class="modal" id="m1">
<div class="modal-box"><h2>When you miss me 💌</h2><p>I miss you too.</p><button class="close" onclick="closeModal('m1')">back</button></div>
</div>

<div class="modal" id="m2">
<div class="modal-box"><h2>When you're sad 🥺</h2><p>You are loved more than you know.</p><button class="close" onclick="closeModal('m2')">back</button></div>
</div>

<div class="modal" id="gallery">
<div class="modal-box"><h2>Our Memories 📸</h2>
<div class="gallery">
<img src="user/photo1.jpeg">
<img src="user/photo2.jpeg">
<img src="user/photo3.jpeg">
<img src="user/photo4.jpeg">
</div>
<button class="close" onclick="closeModal('gallery')">back</button>
</div>
</div>

<div class="modal" id="timeline">
<div class="modal-box"><h2>Our Story 💞</h2>
<div class="timeline">
<div class="moment"><img src="user/memory1.jpeg"><p>The day we met</p></div>
<div class="moment"><img src="user/memory2.jpeg"><p>Our first date</p></div>
<div class="moment"><img src="user/memory3.jpeg"><p>Favorite memory</p></div>
<div class="moment">
<video width="100%" controls><source src="user/memoryvideo.mp4" type="video/mp4"></video>
</div>
</div>
<button class="close" onclick="closeModal('timeline')">back</button>
</div>
</div>

<div class="modal" id="video">
<div class="modal-box">
<h2>A message for you 🎥</h2>
<video width="100%" controls>
<source src="user/video.mp4" type="video/mp4">
</video>
<button class="close" onclick="closeModal('video')">back</button>
</div>
</div>

<div class="modal" id="reasons">
<div class="modal-box">
<h2>100 Reasons I Love You 💞</h2>
<div id="reasonsList"></div>
<button class="close" onclick="closeModal('reasons')">back</button>
</div>
</div>

<div class="modal" id="game">
<div class="modal-box">
<h2>Tap the hearts 💖</h2>
<p id="loveNote">tap a heart to reveal a love note</p>
<button class="btn" onclick="reveal()">💗</button> 
<button class="btn" onclick="reveal()">💗</button> 
<button class="btn" onclick="reveal()">💗</button>
<button class="close" onclick="closeModal('game')">back</button>
</div>
</div>

<script>
function unlock(){document.getElementById("lockscreen").style.display="none";music.play();}
function next(n){document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));document.getElementById('s'+n).classList.add('active');}
function openModal(id){document.getElementById(id).style.display='flex';confetti();}
function closeModal(id){document.getElementById(id).style.display='none';}
let music=document.getElementById("music");
function toggleMusic(){music.paused?music.play():music.pause();}
function toggleDark(){document.body.classList.toggle("dark");}
function shootingStar(){if(!document.body.classList.contains("dark")) return;let star=document.createElement("div");star.className="star";star.style.left=Math.random()*100+"vw";document.body.appendChild(star);setTimeout(()=>star.remove(),2000);}
setInterval(shootingStar,3000);
function createHeart(){let heart=document.createElement("div");heart.className="heart";heart.innerHTML="❤️";heart.style.left=Math.random()*100+"vw";heart.style.fontSize=(Math.random()*20+15)+"px";document.body.appendChild(heart);setTimeout(()=>heart.remove(),8000);}
setInterval(createHeart,600);
function createBlossom(){let blossom=document.createElement("div");blossom.innerHTML="🌸";blossom.style.position="fixed";blossom.style.top="-10px";blossom.style.left=Math.random()*100+"vw";blossom.style.fontSize=(Math.random()*20+15)+"px";blossom.style.animation="fallBlossom 10s linear";document.body.appendChild(blossom);setTimeout(()=>blossom.remove(),10000);}
setInterval(createBlossom,1200);
function confetti(){for(let i=0;i<40;i++){let c=document.createElement("div");c.className="confetti";c.style.left=Math.random()*100+"vw";c.style.backgroundColor=["#ff8fab","#ffd6e0","#ffc2d1","#fff"][Math.floor(Math.random()*4)];document.body.appendChild(c);setTimeout(()=>c.remove(),3000);}}
let cursor=document.createElement("div");cursor.className="cursor-heart";cursor.innerHTML="💗";document.body.appendChild(cursor);document.addEventListener("mousemove",(e)=>{cursor.style.left=e.clientX+"px";cursor.style.top=e.clientY+"px";});
let text="I love you more than words can explain 💖";let i=0;function typeText(){if(i<text.length){document.getElementById("typing").innerHTML+=text.charAt(i);i++;setTimeout(typeText,60);}}typeText();
function openSecret(){let pass=prompt("enter our special word");if(pass==="2311"){alert("I love you more than words can say 💖");}else{alert("wrong password 🥺");}}
let notes=["You make my world brighter","I love your smile","You mean everything to me","I feel lucky to have you"];
function reveal(){let note=notes[Math.floor(Math.random()*notes.length)];document.getElementById("loveNote").innerText=note;}
let reasons=["your smile","your laugh","your kindness","your hugs","your eyes"];
let container=document.getElementById("reasonsList");reasons.forEach((r,i)=>{let p=document.createElement("p");p.innerHTML=(i+1)+". I love "+r;container.appendChild(p);});
</script>

</body>
</html>
