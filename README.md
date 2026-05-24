<!DOCTYPE html>
<html lang="ht">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>XBET Mini Pari</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{
background:
linear-gradient(rgba(0,0,0,.75),rgba(0,0,0,.85)),
url('https://images.unsplash.com/photo-1540747913346-19e32dc3e97e');
background-size:cover;
color:white;
min-height:100vh;
}

.container{
max-width:500px;
margin:auto;
padding:20px;
}

.card{
background:rgba(255,255,255,.08);
backdrop-filter:blur(10px);
padding:20px;
border-radius:20px;
margin-top:20px;
}

h1{
text-align:center;
color:#00d9ff;
margin-bottom:20px;
}

.match{
font-size:22px;
text-align:center;
margin-bottom:10px;
}

.timer{
text-align:center;
color:gold;
margin-bottom:20px;
font-size:18px;
}

.players{
font-size:14px;
margin-bottom:20px;
opacity:.9;
}

.odds{
display:flex;
gap:10px;
margin-bottom:20px;
}

.odd{
flex:1;
padding:15px;
background:#111827;
text-align:center;
border-radius:12px;
cursor:pointer;
border:2px solid transparent;
}

.odd.active{
border-color:#00d9ff;
}

input{
width:100%;
padding:12px;
margin-bottom:10px;
border:none;
border-radius:10px;
}

button{
width:100%;
padding:14px;
background:#00d9ff;
border:none;
border-radius:10px;
font-weight:bold;
cursor:pointer;
}

.info{
margin-top:15px;
text-align:center;
}

.hidden{
display:none;
}

.admin{
margin-top:25px;
border-top:1px solid rgba(255,255,255,.2);
padding-top:20px;
}

.small{
font-size:13px;
opacity:.8;
margin-bottom:8px;
}
</style>
</head>
<body>

<div class="container">

<h1>⚽ XBET MINI PARI</h1>

<div class="card">

<div class="match" id="matchName">
MED 3 et 4 vs MED 1B
</div>

<div class="timer" id="timer"></div>

<div class="players">
<b>Jwè MED 3 et 4:</b>
<span id="players1">7, 10, 11, 15</span>
<br><br>
<b>Jwè MED 1B:</b>
<span id="players2">4, 8, 9, 13</span>
</div>

<div class="odds">
<div class="odd" onclick="choose('MED 3 et 4',this)">
MED 3 et 4<br><b>1.75</b>
</div>

<div class="odd" onclick="choose('MED 1B',this)">
MED 1B<br><b>2.10</b>
</div>
</div>

<input id="amount" type="number" placeholder="Antre kantite HTG">

<button onclick="bet()">PARIER</button>

<div class="info" id="msg"></div>

<div class="info">
👥 Moun ki parye: <span id="betCount">0</span>
</div>

</div>

<div class="card admin">

<h3>🔐 Login Admin</h3>

<input id="adminPass" type="password" placeholder="Modpas">

<button onclick="login()">Antre</button>

<div id="panel" class="hidden">

<hr style="margin:20px 0;">

<div class="small">Chanje match</div>

<input id="team1" placeholder="Ekip 1">
<input id="team2" placeholder="Ekip 2">

<div class="small">Jwè ekip 1 (eg: 7,10,15)</div>
<input id="team1players">

<div class="small">Jwè ekip 2</div>
<input id="team2players">

<div class="small">Dat ak lè match</div>
<input id="matchDate" type="datetime-local">

<button onclick="updateMatch()">Ajoute / Mete ajou match</button>

</div>

</div>

</div>

<script>
let selected="";
let count=localStorage.getItem("bets")||0;
document.getElementById("betCount").innerText=count;

function choose(team,el){
selected=team;

document.querySelectorAll(".odd").forEach(x=>{
x.classList.remove("active");
});

el.classList.add("active");
}

function bet(){

let amount=document.getElementById("amount").value;

if(selected=="" || amount==""){
alert("Chwazi ekip + mete kantite HTG");
return;
}

count++;
localStorage.setItem("bets",count);

document.getElementById("betCount").innerText=count;

document.getElementById("msg").innerHTML=
"✅ Paryaj konfime sou <b>"+selected+
"</b> pou <b>"+amount+" HTG</b>";

document.getElementById("amount").value="";
}

function login(){

let pass=document.getElementById("adminPass").value;

if(pass==="12345"){
document.getElementById("panel")
.classList.remove("hidden");
}else{
alert("Modpas pa bon");
}
}

let savedDate=null;

function updateMatch(){

let t1=document.getElementById("team1").value;
let t2=document.getElementById("team2").value;
let p1=document.getElementById("team1players").value;
let p2=document.getElementById("team2players").value;
let d=document.getElementById("matchDate").value;

if(t1 && t2){
document.getElementById("matchName")
.innerText=t1+" vs "+t2;
}

if(p1){
document.getElementById("players1")
.innerText=p1;
}

if(p2){
document.getElementById("players2")
.innerText=p2;
}

if(d){
savedDate=new Date(d);
}

alert("Match mete ajou!");
}

function timer(){

if(!savedDate){
document.getElementById("timer")
.innerText="Ajoute dat match la";
return;
}

let now=new Date();
let diff=savedDate-now;

if(diff<=0){
document.getElementById("timer")
.innerText="⏰ Match kòmanse!";
return;
}

let h=Math.floor(diff/1000/60/60);
let m=Math.floor(diff/1000/60)%60;
let s=Math.floor(diff/1000)%60;

document.getElementById("timer")
.innerText="Kòmanse nan: "
+h+"h "+m+"m "+s+"s";
}

setInterval(timer,1000);
</script>

</body>
</html>
