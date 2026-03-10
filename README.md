
<html>
<head>

<title>Food Nutrition Analyzer </title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>

body{
font-family:Arial;
margin:0;
background:#f2f2f2;
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

/* MAIN PAGE */

#mainPage{
display:none;
text-align:center;
padding:20px;
min-height:100vh;
background:url("https://images.unsplash.com/photo-1498837167922-ddd27525d352");
background-size:cover;
}

/* TITLE */

.title{
font-size:40px;
font-weight:bold;
color:#111;
margin-bottom:20px;
}

/* BUTTON */

button{
padding:10px 20px;
background:green;
color:white;
border:none;
border-radius:5px;
cursor:pointer;
margin:5px;
}

/* DARK MODE */

.dark{
background:#121212;
color:white;
}

.dark .title{
color:white;
}

/* RESULT BOX */

#result,#bmiResult{
margin-top:20px;
background:rgba(255,255,255,0.9);
padding:15px;
border-radius:10px;
display:inline-block;
font-size:18px;
}

canvas{
max-width:400px;
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

<div class="title">
Food Nutrition Analyzer Using ML
</div>

<button onclick="darkMode()">🌙 Dark Mode</button>
<button onclick="logout()">Logout</button>

<br><br>

<h3>BMI Calculator</h3>

<input id="height" placeholder="Height cm">
<input id="weight" placeholder="Weight kg">

<button onclick="bmi()">Calculate BMI</button>

<div id="bmiResult"></div>

<br><br>

<h3>Food Nutrition Analysis</h3>

<input list="foodList" id="foodName" placeholder="Search Food">

<datalist id="foodList"></datalist>

<br><br>

<button onclick="analyze()">Analyze Food</button>

<div id="result"></div>

<canvas id="chart"></canvas>

</div>

<script>

/* LOGIN */

function login(){

let u=document.getElementById("user").value
let p=document.getElementById("pass").value

if(u!="" && p!=""){

document.getElementById("loginPage").style.display="none"
document.getElementById("mainPage").style.display="block"

}else{

alert("Enter username and password")

}

}

/* LOGOUT */

function logout(){

document.getElementById("mainPage").style.display="none"
document.getElementById("loginPage").style.display="flex"

}

/* DARK MODE */

function darkMode(){
document.body.classList.toggle("dark")
}

/* FOOD DATA */

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

"veg biryani":{cal:250,protein:7},
"chicken biryani":{cal:290,protein:15},
"mutton biryani":{cal:320,protein:18},
"chapati":{cal:104,protein:3},
"parotta":{cal:300,protein:6},
"poori":{cal:250,protein:5},

"paneer butter masala":{cal:300,protein:10},
"palak paneer":{cal:280,protein:11},
"rajma":{cal:240,protein:9},
"dal tadka":{cal:180,protein:8},

"omelette":{cal:155,protein:11},
"boiled egg":{cal:78,protein:6},
"fish curry":{cal:220,protein:20}

}

/* AUTOCOMPLETE */

let list=document.getElementById("foodList")

for(let f in foods){

let option=document.createElement("option")
option.value=f
list.appendChild(option)

}

/* BMI STATUS */

let bmiStatus=""

/* BMI FUNCTION */

function bmi(){

let h=document.getElementById("height").value/100
let w=document.getElementById("weight").value

if(h==0 || w==0){

document.getElementById("bmiResult").innerHTML="Enter valid height and weight"
return

}

let b=w/(h*h)

if(b<18.5){
bmiStatus="underweight"
}
else if(b<25){
bmiStatus="normal"
}
else if(b<30){
bmiStatus="overweight"
}
else{
bmiStatus="obese"
}

document.getElementById("bmiResult").innerHTML=

"<h3>BMI : "+b.toFixed(2)+"</h3>"+
"<p>Status : "+bmiStatus+"</p>"

}

/* FOOD ANALYSIS */

function analyze(){

if(bmiStatus==""){
alert("Please calculate BMI first")
return
}

let f=document.getElementById("foodName").value.toLowerCase()

if(!foods[f]){

document.getElementById("result").innerHTML="Food not found"
return

}

let cal=foods[f].cal
let protein=foods[f].protein

let recommendation=""

if(bmiStatus=="underweight"){

if(cal>200){
recommendation="Recommended for weight gain"
}else{
recommendation="Eat more calorie foods for weight gain"
}

}

else if(bmiStatus=="normal"){

recommendation="Safe to eat in moderation"

}

else if(bmiStatus=="overweight" || bmiStatus=="obese"){

if(cal>200){
recommendation="Not recommended for high weight"
}else{
recommendation="Better food choice for weight control"
}

}

document.getElementById("result").innerHTML=

"<h2>"+f+"</h2>"+
"<p>Calories : "+cal+" kcal</p>"+
"<p>Protein : "+protein+" g</p>"+
"<p>AI Recommendation : "+recommendation+"</p>"

/* GRAPH */

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

</script>

</body>
</html>
