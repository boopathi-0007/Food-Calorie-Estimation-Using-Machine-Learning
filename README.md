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
width:250px;
}

input{
padding:10px;
width:200px;
margin:5px;
}

button{
padding:10px 20px;
background:green;
color:white;
border:none;
cursor:pointer;
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

<!-- LOGIN PAGE -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input type="text" id="username" placeholder="Username"><br>
<input type="password" id="password" placeholder="Password"><br>

<button onclick="login()">Login</button>

</div>

</div>

<!-- MAIN PAGE -->

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<button onclick="toggleDark()">🌙 Dark Mode</button>

<h3>Search Food</h3>

<input list="foodList" id="foodInput" placeholder="Type food name">

<datalist id="foodList"></datalist>

<br><br>

<button onclick="analyze()">Analyze Food</button>

<div id="result"></div>

<h3>Nutrition Chart</h3>

<canvas id="chart"></canvas>

<hr>

<h2>BMI Calculator</h2>

<input id="weight" placeholder="Weight (kg)">
<br>
<input id="height" placeholder="Height (cm)">
<br><br>

<button onclick="calculateBMI()">Calculate BMI</button>

<div id="bmiResult"></div>

<div id="recommend"></div>

</div>


<script>

/* LOGIN FUNCTION */

function login(){

let user=document.getElementById("username").value
let pass=document.getElementById("password").value

if(user==="admin" && pass==="1234"){

document.getElementById("loginPage").style.display="none"
document.getElementById("mainPage").style.display="block"

}else{

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
pakora:{cal:220,protein:5}

}

/* AUTOCOMPLETE */

let list=document.getElementById("foodList")

for(let f in foods){

let option=document.createElement("option")
option.value=f
list.appendChild(option)

}

/* CHART */

let chart

function analyze(){

let f=document.getElementById("foodInput").value

if(!foods[f]){
document.getElementById("result").innerHTML="Food not found"
return
}

let cal=foods[f].cal
let protein=foods[f].protein

document.getElementById("result").innerHTML=

"<h3>"+f+"</h3>"+
"Calories: "+cal+" kcal<br>"+
"Protein: "+protein+" g"

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
rec="Eat milk, banana, paneer"

}
else if(bmi<25){

msg="Normal"
rec="Maintain balanced diet"

}
else if(bmi<30){

msg="Overweight"
rec="Eat salad, idli, soup"

}
else{

msg="Obese"
rec="Reduce calories, eat vegetables"

}

document.getElementById("bmiResult").innerHTML="BMI: "+bmi+" ("+msg+")"

document.getElementById("recommend").innerHTML=rec

}

</script>

</body>
</html>
