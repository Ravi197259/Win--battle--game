<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Win Battle</title>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #111827;
      color: white;
      text-align: center;
    }

    .game {
      max-width: 450px;
      margin: auto;
      padding: 25px 15px;
    }

    h1 {
      margin-top: 20px;
    }

    .coins {
      font-size: 24px;
      margin: 20px;
    }

    .card {
      background: #1f2937;
      padding: 25px;
      border-radius: 20px;
      margin-top: 20px;
    }

    button {
      width: 100%;
      padding: 15px;
      margin: 8px 0;
      border: none;
      border-radius: 12px;
      font-size: 18px;
      cursor: pointer;
    }

    button:hover {
      opacity: .85;
    }

    #message {
      min-height: 30px;
      margin-top: 15px;
      font-size: 18px;
    }
  </style>
</head>

<body>

<div class="game">

  <h1>🏆 Win Battle</h1>

  <div class="coins">
    🪙 Coins: <span id="coins">100</span>
  </div>

  <div class="card">

    <h2 id="question">Question</h2>

    <button onclick="answer(0)" id="a0"></button>
    <button onclick="answer(1)" id="a1"></button>
    <button onclick="answer(2)" id="a2"></button>
    <button onclick="answer(3)" id="a3"></button>

    <div id="message"></div>

  </div>

  <button onclick="newGame()">🔄 New Game</button>

</div>

<script>

let coins = 100;
let currentQuestion = 0;

const questions = [

  {
    q: "भारत की राजधानी क्या है?",
    options: ["मुंबई", "दिल्ली", "जयपुर", "पटना"],
    correct: 1
  },

  {
    q: "2 + 2 कितना होता है?",
    options: ["3", "4", "5", "6"],
    correct: 1
  },

  {
    q: "भारत का राष्ट्रीय पशु कौन है?",
    options: ["शेर", "हाथी", "बाघ", "घोड़ा"],
    correct: 2
  },

  {
    q: "पृथ्वी का उपग्रह कौन है?",
    options: ["सूर्य", "चंद्रमा", "मंगल", "शुक्र"],
    correct: 1
  }

];

function loadQuestion() {

  let q = questions[currentQuestion];

  document.getElementById("question").innerText = q.q;

  for (let i = 0; i < 4; i++) {
    document.getElementById("a" + i).innerText = q.options[i];
  }

  document.getElementById("message").innerText = "";

}

function answer(index) {

  let q = questions[currentQuestion];

  if (index === q.correct) {

    coins += 20;

    document.getElementById("message").innerText =
      "🎉 सही जवाब! +20 Coins";

  } else {

    coins = Math.max(0, coins - 10);

    document.getElementById("message").innerText =
      "❌ गलत जवाब! -10 Coins";

  }

  document.getElementById("coins").innerText = coins;

  currentQuestion++;

  if (currentQuestion >= questions.length) {

    setTimeout(() => {

      alert(
        "🏆 Game Over!\n\nआपके Coins: " + coins
      );

      currentQuestion = 0;
      loadQuestion();

    }, 700);

  } else {

    setTimeout(loadQuestion, 700);

  }

}

function newGame() {

  coins = 100;
  currentQuestion = 0;

  document.getElementById("coins").innerText = coins;

  loadQuestion();

}

loadQuestion();

</script>

</body><!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Win Battle PRO</title>

<style>
*{box-sizing:border-box}
body{
 margin:0;
 font-family:Arial,sans-serif;
 background:#101827;
 color:white;
}
.app{
 max-width:480px;
 margin:auto;
 padding:18px;
}
header{
 text-align:center;
}
h1{
 font-size:34px;
 margin:10px 0;
}
.name{
 display:flex;
 gap:8px;
 margin:15px 0;
}
input{
 flex:1;
 padding:13px;
 border:0;
 border-radius:12px;
 font-size:16px;
}
button{
 border:0;
 border-radius:13px;
 padding:14px;
 font-size:17px;
 cursor:pointer;
}
.start{
 background:#22c55e;
 color:white;
}
.stats{
 display:grid;
 grid-template-columns:repeat(3,1fr);
 gap:8px;
 margin:15px 0;
}
.stat{
 background:#1d293b;
 padding:12px 5px;
 text-align:center;
 border-radius:12px;
}
.card{
 background:#1d293b;
 padding:22px;
 border-radius:22px;
 text-align:center;
}
.timer{
 font-size:28px;
 font-weight:bold;
 margin:10px;
}
.bar{
 height:8px;
 background:#334155;
 border-radius:10px;
 overflow:hidden;
}
.progress{
 height:100%;
 width:100%;
 background:#22c55e;
 transition:width 1s linear;
}
#question{
 min-height:65px;
 font-size:24px;
}
.answer{
 width:100%;
 margin:7px 0;
 background:white;
 color:#111;
}
.answer:disabled{
 opacity:.65;
}
.message{
 min-height:30px;
 margin:10px;
 font-weight:bold;
}
.bottom{
 display:flex;
 gap:8px;
 margin-top:15px;
}
.bottom button{
 flex:1;
 background:#334155;
 color:white;
}
</style>
</head>

<body>

<div class="app">

<header>
<h1>🏆 Win Battle PRO</h1>
</header>

<div class="name">
<input id="playerName" placeholder="अपना नाम लिखें">
<button class="start" onclick="startGame()">START</button>
</div>

<div class="stats">
<div class="stat">🪙<br><b id="coins">100</b></div>
<div class="stat">⭐ Level<br><b id="level">1</b></div>
<div class="stat">🔥 Streak<br><b id="streak">0</b></div>
</div>

<div class="card">

<div>⏱️ <span id="time">15</span> sec</div>

<div class="bar">
<div class="progress" id="progress"></div>
</div>

<h2 id="question">START दबाकर खेल शुरू करें</h2>

<div id="answers"></div>

<div class="message" id="message"></div>

</div>

<div class="bottom">
<button onclick="dailyBonus()">🎁 Daily Bonus</button>
<button onclick="newGame()">🔄 New Game</button>
</div>

</div>

<script>

const questions=[
{
q:"भारत की राजधानी क्या है?",
a:["मुंबई","दिल्ली","जयपुर","पटना"],
c:1
},
{
q:"2 + 2 कितना होता है?",
a:["3","4","5","6"],
c:1
},
{
q:"भारत का राष्ट्रीय पशु कौन है?",
a:["शेर","हाथी","बाघ","घोड़ा"],
c:2
},
{
q:"पृथ्वी का उपग्रह कौन है?",
a:["सूर्य","चंद्रमा","मंगल","शुक्र"],
c:1
},
{
q:"भारत का राष्ट्रीय पक्षी कौन है?",
a:["तोता","मोर","कबूतर","गरुड़"],
c:1
},
{
q:"एक सप्ताह में कितने दिन होते हैं?",
a:["5","6","7","8"],
c:2
},
{
q:"पानी का सूत्र क्या है?",
a:["CO2","H2O","O2","NaCl"],
c:1
},
{
q:"सूर्य किस दिशा से निकलता है?",
a:["पश्चिम","उत्तर","पूर्व","दक्षिण"],
c:2
},
{
q:"10 × 5 कितना है?",
a:["25","40","50","60"],
c:2
},
{
q:"भारत का राष्ट्रीय फूल कौन है?",
a:["गुलाब","कमल","गेंदा","चमेली"],
c:1
}
];

let coins=100;
let level=1;
let streak=0;
let index=0;
let time=15;
let timer=null;
let playing=false;
let score=0;

function startGame(){

 let name=document.getElementById("playerName").value.trim();

 if(!name){
   alert("पहले अपना नाम लिखें!");
   return;
 }

 newGame();
}

function newGame(){

 clearInterval(timer);

 coins=100;
 level=1;
 streak=0;
 index=0;
 score=0;
 playing=true;

 updateStats();
 showQuestion();
}

function showQuestion(){

 if(index>=questions.length){
   finishGame();
   return;
 }

 const q=questions[index];

 document.getElementById("question").innerText=q.q;
 document.getElementById("message").innerText="";
 document.getElementById("answers").innerHTML="";

 q.a.forEach((answer,i)=>{

   const btn=document.createElement("button");

   btn.className="answer";
   btn.innerText=answer;
   btn.onclick=()=>checkAnswer(i);

   document.getElementById("answers").appendChild(btn);

 });

 startTimer();
}

function startTimer(){

 clearInterval(timer);

 time=15;
 updateTimer();

 timer=setInterval(()=>{

   time--;
   updateTimer();

   if(time<=0){

     clearInterval(timer);
     checkAnswer(-1);

   }

 },1000);
}

function updateTimer(){

 document.getElementById("time").innerText=time;

 document.getElementById("progress").style.width=
   (time/15*100)+"%";
}

function checkAnswer(choice){

 if(!playing)return;

 clearInterval(timer);

 const q=questions[index];

 document.querySelectorAll(".answer")
 .forEach(btn=>btn.disabled=true);

 if(choice===q.c){

   streak++;

   const reward=20+(streak*5);

   coins+=reward;
   score+=10;

   document.getElementById("message").innerText=
     "🎉 सही जवाब! +" + reward + " Coins";

 }else{

   streak=0;
   coins=Math.max(0,coins-10);

   document.getElementById("message").innerText=
     choice===-1
     ?"⏰ समय समाप्त! -10 Coins"
     :"❌ गलत जवाब! -10 Coins";
 }

 level=Math.min(10,Math.floor(index/2)+1);

 updateStats();

 index++;

 setTimeout(showQuestion,800);
}

function updateStats(){

 document.getElementById("coins").innerText=coins;
 document.getElementById("level").innerText=level;
 document.getElementById("streak").innerText=streak;
}

function finishGame(){

 playing=false;

 const name=document.getElementById("playerName").value;

 let high=localStorage.getItem("winBattleHighScore")||0;

 if(score>high){

   localStorage.setItem("winBattleHighScore",score);

   high=score;
 }

 alert(
   "🏆 GAME COMPLETE!\n\n"+
   "👤 Player: "+name+"\n"+
   "⭐ Level: "+level+"\n"+
   "🎯 Score: "+score+"\n"+
   "🪙 Coins: "+coins+"\n"+
   "🏆 High Score: "+high
 );

 document.getElementById("question").innerText=
   "🏆 Game Complete!";

 document.getElementById("answers").innerHTML="";

}

function dailyBonus(){

 const today=new Date().toDateString();
 const last=localStorage.getItem("dailyBonus");

 if(last===today){

   alert("🎁 आज का Bonus पहले ही मिल चुका है!");

 }else{

   coins+=50;

   localStorage.setItem("dailyBonus",today);

   updateStats();

   alert("🎁 Daily Bonus!\n\n+50 Virtual Coins");
 }
}

</script>

</body>
</html>
