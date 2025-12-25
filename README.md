# Hackerbendara<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>CRITICAL SYSTEM FAILURE</title>
<style>
body{
  margin:0;
  background:black;
  color:#ff2b2b;
  font-family:monospace;
  overflow:hidden;
}
#screen{
  position:fixed;
  inset:0;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  text-align:center;
}
#title{
  font-size:28px;
  animation:flicker .12s infinite;
}
@keyframes flicker{
  0%{opacity:1}50%{opacity:.2}
}
#text{
  margin-top:20px;
  font-size:18px;
  line-height:1.8;
}
#count{
  margin-top:25px;
  font-size:70px;
}
.shake{
  animation:shake .08s infinite;
}
@keyframes shake{
  0%{transform:translate(0,0)}
  25%{transform:translate(3px,2px)}
  50%{transform:translate(-3px,2px)}
  75%{transform:translate(2px,-2px)}
}
#flash{
  position:fixed;
  inset:0;
  background:red;
  opacity:0;
  pointer-events:none;
  animation:flash 4s infinite;
}
@keyframes flash{
  0%,85%{opacity:0}
  86%,90%{opacity:.9}
  100%{opacity:0}
}
button{
  position:fixed;
  bottom:15px;
  right:15px;
  padding:10px 18px;
  background:black;
  color:#00ff7f;
  border:1px solid #00ff7f;
}
#truth{
  display:none;
  color:#00ff7f;
  font-size:26px;
}
.small{font-size:13px;color:#aaa}
</style>
</head>

<body>

<div id="flash"></div>

<div id="screen">
  <div id="title">⚠️ SYSTEM BREACH DETECTED ⚠️</div>
  <div id="text"></div>
  <div id="count">02:30</div>
  <div id="truth">
    😂 مقلب فقط<br>
    لا اختراق حقيقي<br>
    <span class="small">Visual prank only</span>
  </div>
</div>

<button onclick="stopAll()">⛔ إيقاف</button>

<audio id="beat" loop>
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-fast-heartbeat-1175.mp3">
</audio>
<audio id="alarm" loop>
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-alarm-digital-clock-beep-989.mp3">
</audio>

<script>
let s = 150;
const msgs = [
 "الوصول إلى النظام...",
 "تعطيل الحماية...",
 "فشل الإيقاف...",
 "النظام غير مستجيب...",
 "لا تحاول الخروج...",
 "العد التنازلي بدأ..."
];
let i=0;

const text = document.getElementById("text");
const count = document.getElementById("count");
const beat = document.getElementById("beat");
const alarm = document.getElementById("alarm");
const screen = document.getElementById("screen");

function format(x){
  return String(Math.floor(x/60)).padStart(2,'0')+":"+String(x%60).padStart(2,'0');
}

function start(){
  screen.classList.add("shake");
  beat.volume=0.6; alarm.volume=0.5;
  beat.play(); alarm.play();

  setInterval(()=>{
    if(i < msgs.length){
      text.innerHTML += msgs[i]+"<br>";
      i++;
    }
  },3000);

  setInterval(()=>{
    s--;
    count.textContent=format(s);
    if(s<=0) stopAll();
  },1000);
}

function stopAll(){
  beat.pause(); alarm.pause();
  document.getElementById("title").style.display="none";
  text.style.display="none";
  count.style.display="none";
  document.getElementById("truth").style.display="block";
}

document.body.onclick=start;
</script>

</body>
</html>
