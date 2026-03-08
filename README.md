<!DOCTYPE html>
<html>

<head>

<title>Food Calorie Estimation Using ML</title>

<style>

body{
font-family:Arial;
margin:0;
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

input{
padding:10px;
width:220px;
}

button{
padding:10px 20px;
background:green;
color:white;
border:none;
margin-top:10px;
cursor:pointer;
}

/* MAIN PAGE */

#mainPage{
display:none;
text-align:center;
padding:30px;
background:#f5f5f5;
height:100vh;
}

img{
width:260px;
margin-top:20px;
border-radius:10px;
}

</style>

</head>

<body>

<!-- LOGIN PAGE -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input type="text" id="username" placeholder="Username"><br><br>
<input type="password" id="password" placeholder="Password"><br><br>

<button onclick="login()">Login</button>

</div>

</div>

<!-- MAIN PAGE -->

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<input type="text" id="foodName" placeholder="Example: dosa">

<br><br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

</div>

<script>

/* LOGIN FUNCTION */

function login(){

let user=document.getElementById("username").value;
let pass=document.getElementById("password").value;

if(user=="admin" && pass=="1234"){

document.getElementById("loginPage").style.display="none";
document.getElementById("mainPage").style.display="block";

}
else{

alert("Invalid Login");

}

}

/* FOOD DATASET */

let foods={

idli:{cal:58,protein:2,img:"https://images.unsplash.com/photo-1589301760014-d929f3979dbc"},
dosa:{cal:133,protein:3,img:"https://images.unsplash.com/photo-1630409351217-bc4fa6422075"},
rasam:{cal:60,protein:2,img:"https://images.unsplash.com/photo-1604908176997-431c16c0f5fa"},
sambar:{cal:90,protein:5,img:"https://images.unsplash.com/photo-1604909052743-94e838986d24"},
pongal:{cal:180,protein:6,img:"https://images.unsplash.com/photo-1589302168068-964664d93dc0"},
poha:{cal:180,protein:4,img:"https://images.unsplash.com/photo-1604908812834-5c9f4c7c9f6f"},
chapati:{cal:104,protein:3,img:"https://images.unsplash.com/photo-1617191519000-3f6f7b3c6c13"},
biryani:{cal:290,protein:15,img:"https://images.unsplash.com/photo-1631515243349-e0cb75fb8d3a"},
jalebi:{cal:300,protein:2,img:"https://images.unsplash.com/photo-1601050690597-df0568f70950"},
gulab_jamun:{cal:350,protein:4,img:"https://images.unsplash.com/photo-1603532648955-039310d9ed75"}

};

/* ANALYZE FUNCTION */

function analyze(){

let f=document.getElementById("foodName").value.toLowerCase();

if(!foods[f]){

document.getElementById("result").innerHTML="<h3>Food not found in dataset</h3>";
return;

}

let cal=foods[f].cal;
let protein=foods[f].protein;
let img=foods[f].img;

let category="";
let suggestion="";

if(cal<150){

category="Healthy Food";
suggestion="Good for diet";

}
else if(cal<280){

category="Moderate Food";
suggestion="Eat balanced diet";

}
else{

category="High Calorie Food";
suggestion="Eat occasionally";

}

document.getElementById("result").innerHTML=

"<h2>"+f+"</h2>"+
"<img src='"+img+"'>"+
"<p>Calories: "+cal+" kcal</p>"+
"<p>Protein: "+protein+" g</p>"+
"<p>Category: "+category+"</p>"+
"<p>Suggestion: "+suggestion+"</p>";

}

</script>

</body>
</html>
