<!DOCTYPE html>
<html>
<head>

<title>Indian Food Nutrition Analyzer</title>

<style>

body{
font-family:Arial;
margin:0;
}

#loginPage{
height:100vh;
display:flex;
justify-content:center;
align-items:center;
background-image:url("https://images.unsplash.com/photo-1490645935967-10de6ba17061");
background-size:cover;
}

.loginBox{
background:white;
padding:30px;
border-radius:10px;
text-align:center;
}

#mainPage{
display:none;
text-align:center;
padding:30px;
}

img{
width:260px;
margin-top:20px;
border-radius:10px;
}

button{
padding:10px 20px;
background:green;
color:white;
border:none;
cursor:pointer;
}

input{
padding:10px;
width:220px;
}

</style>

</head>

<body>

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input type="text"><br><br>
<input type="password"><br><br>

<button onclick="login()">Login</button>

</div>

</div>

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<input type="text" id="foodName" placeholder="Example: dosa">

<br><br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

</div>

<script>

function login(){
document.getElementById("loginPage").style.display="none";
document.getElementById("mainPage").style.display="block";
}

let foods={

idli:{cal:58,protein:2},
dosa:{cal:133,protein:3},
pongal:{cal:180,protein:6},
upma:{cal:120,protein:3},
vada:{cal:150,protein:4},
sambar:{cal:90,protein:5},
rasam:{cal:60,protein:2},
curd_rice:{cal:180,protein:6},
lemon_rice:{cal:200,protein:4},
tamarind_rice:{cal:210,protein:4},
veg_biryani:{cal:250,protein:7},
chicken_biryani:{cal:290,protein:15},
mutton_biryani:{cal:320,protein:18},
chapati:{cal:104,protein:3},
parotta:{cal:300,protein:6},
poori:{cal:250,protein:5},
naan:{cal:260,protein:6},
paneer_butter_masala:{cal:300,protein:10},
palak_paneer:{cal:280,protein:11},
rajma:{cal:240,protein:9},
dal_tadka:{cal:180,protein:8},
dal_makhani:{cal:300,protein:10},
aloo_paratha:{cal:260,protein:6},
gobi_paratha:{cal:240,protein:6},
paneer_paratha:{cal:280,protein:9},
veg_samosa:{cal:262,protein:6},
pakora:{cal:220,protein:5},
pav_bhaji:{cal:400,protein:10},
vada_pav:{cal:300,protein:8},
misal_pav:{cal:350,protein:12},
dhokla:{cal:160,protein:6},
thepla:{cal:200,protein:5},
khichdi:{cal:180,protein:6},
poha:{cal:180,protein:4},
jalebi:{cal:300,protein:2},
gulab_jamun:{cal:350,protein:4}

};

function analyze(){

let f=document.getElementById("foodName").value.toLowerCase();

if(!foods[f]){
document.getElementById("result").innerHTML="Food not in dataset";
return;
}

let cal=foods[f].cal;
let protein=foods[f].protein;

let category="";
let suggestion="";
let tip="";

if(cal<150){
category="Healthy Food";
suggestion="Good for diet";
tip="Eat with vegetables";
}
else if(cal<280){
category="Moderate Food";
suggestion="Eat balanced diet";
tip="Drink more water";
}
else{
category="High Calorie Food";
suggestion="Eat occasionally";
tip="Do exercise regularly";
}

/* IMAGE LINK */

let img="https://source.unsplash.com/400x300/?indian,"+f;

document.getElementById("result").innerHTML=

"<h2>"+f+"</h2>"+
"<img src='"+img+"'>"+
"<p>Calories : "+cal+" kcal</p>"+
"<p>Protein : "+protein+" g</p>"+
"<p>Category : "+category+"</p>"+
"<p>Suggestion : "+suggestion+"</p>"+
"<p>Health Tip : "+tip+"</p>";

}

</script>

</body>
</html>
