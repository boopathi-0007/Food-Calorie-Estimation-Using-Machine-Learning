<!DOCTYPE html>
<html>
<head>
<title>Indian Food Nutrition Analyzer</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>

body{
font-family:Arial;
margin:0;
background:#f2f2f2;
transition:0.4s;
}

/* LOGIN PAGE */

#loginPage{
height:100vh;
display:flex;
justify-content:center;
align-items:center;
background:url("https://images.unsplash.com/photo-1490645935967-10de6ba17061");
background-size:cover;
}

/* LOGIN BOX */

.loginBox{
background:white;
padding:30px;
border-radius:10px;
text-align:center;
box-shadow:0 0 10px rgba(0,0,0,0.3);
}

.loginBox input{
padding:10px;
width:200px;
}

/* BUTTON */

button{
padding:10px 20px;
background:green;
color:white;
border:none;
cursor:pointer;
border-radius:5px;
}

/* MAIN PAGE */

#mainPage{
display:none;
padding:20px;
text-align:center;
min-height:100vh;
background:url("https://images.unsplash.com/photo-1498837167922-ddd27525d352");
background-size:cover;
background-position:center;
}

/* DARK MODE */

.dark{
background:#121212;
color:white;
}

.dark input{
background:#333;
color:white;
}

.dark button{
background:#444;
}

/* RESULT */

#result{
margin-top:20px;
font-size:18px;
background:rgba(255,255,255,0.85);
padding:15px;
border-radius:10px;
display:inline-block;
}

#bmiResult{
margin-top:20px;
background:rgba(255,255,255,0.85);
padding:10px;
border-radius:10px;
display:inline-block;
}

canvas{
max-width:400px;
margin:auto;
margin-top:20px;
background:white;
padding:10px;
border-radius:10px;
}

</style>
</head>

<body>

<!-- LOGIN PAGE -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input id="user" placeholder="Username"><br><br>

<input id="pass" type="password" placeholder="Password"><br><br>

<button onclick="login()">Login</button>

</div>

</div>

<!-- MAIN PAGE -->

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<button onclick="darkMode()">🌙 Dark Mode</button>

<br><br>

<!-- FOOD SEARCH -->

<input list="foodList" id="foodName" placeholder="Search Food">

<datalist id="foodList"></datalist>

<br><br>

<button onclick="analyze()">Analyze Food</button>

<!-- FOOD RESULT -->

<div id="result"></div>

<canvas id="chart"></canvas>

<br><br>

<!-- BMI CALCULATOR AFTER FOOD RESULT -->

<h3>BMI Calculator</h3>

<input id="height" placeholder="Height cm">
<input id="weight" placeholder="Weight kg">

<button onclick="bmi()">Check BMI</button>

<div id="bmiResult"></div>

</div>

<script>

/* LOGIN */

function login(){

let u=document.getElementById("user").value
let p=document.getElementById("pass").value

if(u!="" && p!=""){

document.getElementById("loginPage").style.display="none"
document.getElementById("mainPage").style.display="block"

}
else{

alert("Enter username and password")

}

}

/* DARK MODE */

function darkMode(){

document.body.classList.toggle("dark")

}

/* FOOD DATASET */

let foods={

"idli":{cal:58,protein:2},
"dosa":{cal:133,protein:3},
"masala dosa":{cal:230,protein:5},
"pongal":{cal:180,protein:6},
"upma":{cal:120,protein:3},
"vada":{cal:150,protein:4},
"sambar":{cal:90,protein:5},
"rasam":{cal:60,protein:2},
"curd rice":{cal:180,protein:6},
"lemon rice":{cal:200,protein:4},

"tamarind rice":{cal:210,protein:4},
"veg biryani":{cal:250,protein:7},
"chicken biryani":{cal:290,protein:15},
"mutton biryani":{cal:320,protein:18},
"chapati":{cal:104,protein:3},
"parotta":{cal:300,protein:6},
"poori":{cal:250,protein:5},
"naan":{cal:260,protein:6},
"paneer butter masala":{cal:300,protein:10},
"palak paneer":{cal:280,protein:11},

"rajma":{cal:240,protein:9},
"dal tadka":{cal:180,protein:8},
"dal makhani":{cal:300,protein:10},
"aloo paratha":{cal:260,protein:6},
"gobi paratha":{cal:240,protein:6},
"paneer paratha":{cal:280,protein:9},
"veg samosa":{cal:262,protein:6},
"pakora":{cal:220,protein:5},
"pav bhaji":{cal:400,protein:10},
"vada pav":{cal:300,protein:8},

"misal pav":{cal:350,protein:12},
"dhokla":{cal:160,protein:6},
"thepla":{cal:200,protein:5},
"khichdi":{cal:180,protein:6},
"poha":{cal:180,protein:4},
"jalebi":{cal:300,protein:2},
"gulab jamun":{cal:350,protein:4},
"kheer":{cal:220,protein:6},
"ladoo":{cal:300,protein:5},
"halwa":{cal:250,protein:4},

"butter chicken":{cal:490,protein:25},
"tandoori chicken":{cal:300,protein:35},
"egg curry":{cal:180,protein:12},
"omelette":{cal:155,protein:11},
"boiled egg":{cal:78,protein:6},
"fish curry":{cal:220,protein:20},
"pani puri":{cal:180,protein:4},
"bhel puri":{cal:170,protein:5},
"sev puri":{cal:200,protein:5},
"kathi roll":{cal:330,protein:12}

}

/* AUTOCOMPLETE */

let list=document.getElementById("foodList")

for(let f in foods){

let option=document.createElement("option")
option.value=f
list.appendChild(option)

}

/* FOOD ANALYZER */

function analyze(){

let f=document.getElementById("foodName").value.toLowerCase()

if(!foods[f]){
document.getElementById("result").innerHTML="Food not found"
return
}

let cal=foods[f].cal
let protein=foods[f].protein

let recommendation=""

if(cal<150){
recommendation="Good for weight loss"
}
else if(cal<300){
recommendation="Eat in moderation"
}
else{
recommendation="High calorie food"
}

document.getElementById("result").innerHTML=

"<h2>"+f+"</h2>"+
"<p>Calories : "+cal+" kcal</p>"+
"<p>Protein : "+protein+" g</p>"+
"<p>AI Recommendation : "+recommendation+"</p>"

let ctx=document.getElementById("chart")

new Chart(ctx,{
type:'bar',
data:{
labels:['Calories','Protein'],
datasets:[{
label:f,
data:[cal,protein]
}]
}
})

}

/* BMI */

function bmi(){

let h=document.getElementById("height").value/100
let w=document.getElementById("weight").value

if(h==0 || w==0){
document.getElementById("bmiResult").innerHTML="Enter valid height and weight"
return
}

let b=w/(h*h)

let status=""
let suggestion=""

if(b<18.5){
status="Underweight"
suggestion="Increase calorie intake. Eat rice, milk, eggs, banana and nuts."
}
else if(b>=18.5 && b<25){
status="Normal Weight"
suggestion="Maintain balanced diet and regular exercise."
}
else if(b>=25 && b<30){
status="Overweight"
suggestion="Reduce oily foods and sweets. Eat vegetables and exercise."
}
else{
status="Obese"
suggestion="Avoid junk food and high calorie foods. Follow strict healthy diet."
}

document.getElementById("bmiResult").innerHTML=

"<h3>BMI : "+b.toFixed(2)+"</h3>"+
"<p>Status : "+status+"</p>"+
"<p>Diet Suggestion : "+suggestion+"</p>"

}

</script>

</body>
</html>
