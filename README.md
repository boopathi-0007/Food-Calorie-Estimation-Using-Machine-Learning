<!DOCTYPE html>
<html>
<head>

<title>Indian Food Nutrition Analyzer</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>

body{
font-family:Arial;
margin:0;
background:#f5f5f5;
color:black;
}

/* LOGIN PAGE */

#loginPage{
height:100vh;
display:flex;
justify-content:center;
align-items:center;
background-image:url("https://images.unsplash.com/photo-1504674900247-0877df9cc836");
background-size:cover;
}

.loginBox{
background:white;
padding:30px;
border-radius:10px;
text-align:center;
}

input,select{
padding:10px;
width:220px;
margin:5px;
}

button{
padding:10px 20px;
background:green;
color:white;
border:none;
cursor:pointer;
margin-top:10px;
}

#mainPage{
display:none;
text-align:center;
padding:30px;
min-height:100vh;
}

.dark{
background:#111;
color:white;
}

canvas{
max-width:500px;
margin:auto;
}

</style>

</head>

<body>

<!-- LOGIN -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input id="user" placeholder="Username"><br>
<input id="pass" type="password" placeholder="Password"><br>

<button onclick="login()">Login</button>

</div>

</div>


<!-- MAIN PAGE -->

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<button onclick="toggleDark()">🌙 Dark Mode</button>

<h3>Search Food</h3>

<input list="foodsList" id="foodInput" placeholder="Type food name">

<datalist id="foodsList"></datalist>

<br>

<button onclick="analyze()">Analyze Food</button>

<div id="result"></div>

<h3>Nutrition Chart</h3>

<canvas id="chart"></canvas>

<hr>

<h2>BMI Calculator</h2>

<input id="weight" placeholder="Weight (kg)">
<br>
<input id="height" placeholder="Height (cm)">
<br>

<button onclick="calculateBMI()">Calculate BMI</button>

<div id="bmiResult"></div>

<div id="recommend"></div>

</div>


<script>

/* LOGIN */

function login(){

let u=document.getElementById("user").value
let p=document.getElementById("pass").value

if(u=="admin" && p=="1234"){

document.getElementById("loginPage").style.display="none"
document.getElementById("mainPage").style.display="block"

}
else{

alert("Invalid Login")

}

}

/* DARK MODE */

function toggleDark(){

document.body.classList.toggle("dark")

}

/* FOOD DATASET */

let foods={
biryani:{cal:290,protein:15},
dosa:{cal:133,protein:3},
idli:{cal:58,protein:2},
sambar:{cal:90,protein:5},
rasam:{cal:60,protein:2},
pongal:{cal:180,protein:6},
upma:{cal:120,protein:3},
poha:{cal:180,protein:4},
chapati:{cal:104,protein:3},
naan:{cal:260,protein:6},
parotta:{cal:300,protein:6},
poori:{cal:250,protein:5},
pulao:{cal:220,protein:6},
lemon_rice:{cal:200,protein:4},
curd_rice:{cal:180,protein:6},
rajma:{cal:240,protein:9},
dal:{cal:180,protein:8},
paneer:{cal:300,protein:10},
samosa:{cal:262,protein:6},
pakora:{cal:220,protein:5},
pav_bhaji:{cal:400,protein:10},
vada_pav:{cal:300,protein:8},
dhokla:{cal:160,protein:6},
khichdi:{cal:180,protein:6},
jalebi:{cal:300,protein:2},
gulab_jamun:{cal:350,protein:4},
kheer:{cal:250,protein:6},
laddu:{cal:280,protein:5},
halwa:{cal:290,protein:4},
mysore_pak:{cal:310,protein:4},
butter_chicken:{cal:300,protein:20},
tandoori_chicken:{cal:220,protein:25},
fish_curry:{cal:200,protein:22},
egg_curry:{cal:180,protein:13},
fried_rice:{cal:230,protein:6},
noodles:{cal:220,protein:5},
maggi:{cal:205,protein:4},
chole_bhature:{cal:350,protein:12},
aloo_paratha:{cal:260,protein:6},
gobi_paratha:{cal:240,protein:6},
paneer_paratha:{cal:280,protein:9},
veg_roll:{cal:210,protein:5},
chicken_roll:{cal:260,protein:12},
paneer_roll:{cal:240,protein:9},
veg_cutlet:{cal:180,protein:4},
bread_omelette:{cal:200,protein:10},
omelette:{cal:150,protein:11},
milk:{cal:120,protein:8},
curd:{cal:98,protein:5},
banana:{cal:105,protein:1},
apple:{cal:95,protein:1},
orange:{cal:62,protein:1},
mango:{cal:150,protein:2},
grapes:{cal:104,protein:1},
watermelon:{cal:85,protein:1},
papaya:{cal:120,protein:1},
pineapple:{cal:82,protein:1},
carrot:{cal:41,protein:1},
beetroot:{cal:43,protein:2},
potato:{cal:163,protein:4},
spinach:{cal:23,protein:3}
}

/* AUTOCOMPLETE LOAD */

let list=document.getElementById("foodsList")

for(let f in foods){

let option=document.createElement("option")
option.value=f
list.appendChild(option)

}

/* ANALYZE */

let chart

function analyze(){

let f=document.getElementById("foodInput").value

if(!foods[f]){

document.getElementById("result").innerHTML="Food not found"
return

}

let cal=foods[f].cal
let protein=foods[f].protein

let category=""

if(cal<150){category="Healthy"}
else if(cal<280){category="Moderate"}
else{category="High Calorie"}

document.getElementById("result").innerHTML=

"<h3>"+f+"</h3>"+
"Calories: "+cal+" kcal<br>"+
"Protein: "+protein+" g<br>"+
"Category: "+category

if(chart){chart.destroy()}

chart=new Chart(document.getElementById("chart"),{

type:"bar",

data:{
labels:["Calories","Protein"],
datasets:[{
label:f,
data:[cal,protein]
}]
}

})

}

/* BMI */

function calculateBMI(){

let w=document.getElementById("weight").value
let h=document.getElementById("height").value/100

let bmi=(w/(h*h)).toFixed(1)

let msg=""
let rec=""

if(bmi<18.5){

msg="Underweight"
rec="Recommended: milk, paneer, banana, egg"

}

else if(bmi<25){

msg="Normal"
rec="Recommended: chapati, dal, fruits"

}

else if(bmi<30){

msg="Overweight"
rec="Recommended: salad, idli, vegetable soup"

}

else{

msg="Obese"
rec="Recommended: spinach, soup, fruits"

}

document.getElementById("bmiResult").innerHTML=

"BMI: "+bmi+" ("+msg+")"

document.getElementById("recommend").innerHTML=

rec

}

</script>

</body>
</html>
