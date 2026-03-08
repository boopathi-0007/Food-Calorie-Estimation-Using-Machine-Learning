<!DOCTYPE html>
<html>
<head>

<title>Food Calorie Estimation</title>

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

<!-- LOGIN -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input type="text" id="user" placeholder="Username"><br><br>
<input type="password" id="pass" placeholder="Password"><br><br>

<button onclick="login()">Login</button>

</div>

</div>


<!-- MAIN -->

<div id="mainPage">

<h1>Indian Food Nutrition Analyzer</h1>

<input type="text" id="foodName" placeholder="Example: biryani">

<br><br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

</div>


<script>

/* LOGIN */

function login(){

let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u=="admin" && p=="1234"){

document.getElementById("loginPage").style.display="none";
document.getElementById("mainPage").style.display="block";

}
else{

alert("Invalid Login");

}

}


/* DATASET 30 FOODS */

let foods={

biryani:{cal:290,protein:15,img:"https://source.unsplash.com/400x300/?biryani"},
dosa:{cal:133,protein:3,img:"https://source.unsplash.com/400x300/?dosa"},
idli:{cal:58,protein:2,img:"https://source.unsplash.com/400x300/?idli"},
sambar:{cal:90,protein:5,img:"https://source.unsplash.com/400x300/?sambar"},
rasam:{cal:60,protein:2,img:"https://source.unsplash.com/400x300/?rasam"},
pongal:{cal:180,protein:6,img:"https://source.unsplash.com/400x300/?pongal"},
upma:{cal:120,protein:3,img:"https://source.unsplash.com/400x300/?upma"},
poha:{cal:180,protein:4,img:"https://source.unsplash.com/400x300/?poha"},
chapati:{cal:104,protein:3,img:"https://source.unsplash.com/400x300/?chapati"},
naan:{cal:260,protein:6,img:"https://source.unsplash.com/400x300/?naan"},

parotta:{cal:300,protein:6,img:"https://source.unsplash.com/400x300/?parotta"},
poori:{cal:250,protein:5,img:"https://source.unsplash.com/400x300/?poori"},
veg_biryani:{cal:250,protein:7,img:"https://source.unsplash.com/400x300/?veg-biryani"},
chicken_biryani:{cal:290,protein:15,img:"https://source.unsplash.com/400x300/?chicken-biryani"},
pulao:{cal:220,protein:6,img:"https://source.unsplash.com/400x300/?pulao"},
lemon_rice:{cal:200,protein:4,img:"https://source.unsplash.com/400x300/?lemon-rice"},
curd_rice:{cal:180,protein:6,img:"https://source.unsplash.com/400x300/?curd-rice"},
rajma:{cal:240,protein:9,img:"https://source.unsplash.com/400x300/?rajma"},
dal:{cal:180,protein:8,img:"https://source.unsplash.com/400x300/?dal"},
paneer:{cal:300,protein:10,img:"https://source.unsplash.com/400x300/?paneer"},

samosa:{cal:262,protein:6,img:"https://source.unsplash.com/400x300/?samosa"},
pakora:{cal:220,protein:5,img:"https://source.unsplash.com/400x300/?pakora"},
pav_bhaji:{cal:400,protein:10,img:"https://source.unsplash.com/400x300/?pav-bhaji"},
vada_pav:{cal:300,protein:8,img:"https://source.unsplash.com/400x300/?vada-pav"},
dhokla:{cal:160,protein:6,img:"https://source.unsplash.com/400x300/?dhokla"},
khichdi:{cal:180,protein:6,img:"https://source.unsplash.com/400x300/?khichdi"},
jalebi:{cal:300,protein:2,img:"https://source.unsplash.com/400x300/?jalebi"},
gulab_jamun:{cal:350,protein:4,img:"https://source.unsplash.com/400x300/?gulab-jamun"},
kheer:{cal:250,protein:6,img:"https://source.unsplash.com/400x300/?kheer"},
laddu:{cal:280,protein:5,img:"https://source.unsplash.com/400x300/?laddu"}

};


/* ANALYZE */

function analyze(){

let f=document.getElementById("foodName").value.toLowerCase();

if(!foods[f]){

document.getElementById("result").innerHTML="<h3>Food not found</h3>";
return;

}

let cal=foods[f].cal;
let protein=foods[f].protein;
let img=foods[f].img;

let category="";
let suggestion="";
let tip="";

if(cal<150){

category="Healthy Food";
suggestion="Good for diet";
tip="Eat more vegetables";

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

document.getElementById("result").innerHTML=

"<h2>"+f+"</h2>"+
"<img src='"+img+"'>"+
"<p><b>Calories:</b> "+cal+" kcal</p>"+
"<p><b>Protein:</b> "+protein+" g</p>"+
"<p><b>Category:</b> "+category+"</p>"+
"<p><b>Suggestion:</b> "+suggestion+"</p>"+
"<p><b>Health Tip:</b> "+tip+"</p>";

}

</script>

</body>
</html>
