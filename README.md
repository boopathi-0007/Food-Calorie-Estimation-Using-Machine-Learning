<!DOCTYPE html>
<html>
<head>
<title>AI Food Nutrition Analyzer</title>

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
background-image:url("https://images.unsplash.com/photo-1490645935967-10de6ba17061");
background-size:cover;
}

.loginBox{
background:white;
padding:30px;
border-radius:10px;
text-align:center;
box-shadow:0 0 10px gray;
}

input{
padding:10px;
margin:10px;
width:200px;
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
}

.result{
margin-top:20px;
font-size:18px;
}

</style>

</head>

<body>

<!-- LOGIN PAGE -->

<div id="loginPage">

<div class="loginBox">

<h2>Login</h2>

<input type="text" id="user" placeholder="Username"><br>

<input type="password" id="pass" placeholder="Password"><br>

<button onclick="login()">Login</button>

</div>

</div>


<!-- MAIN PAGE -->

<div id="mainPage">

<h1>AI Food Nutrition Analyzer</h1>

<p>Upload Food Image</p>

<input type="file" id="image">

<br><br>

<button onclick="analyzeFood()">Analyze</button>

<div class="result" id="output"></div>

</div>


<script>

/* LOGIN */

function login(){

let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u=="admin" && p=="1234")
{
document.getElementById("loginPage").style.display="none";
document.getElementById("mainPage").style.display="block";
}
else
{
alert("Invalid Login");
}

}


/* DATASET */

let foods={

apple:{cal:52,protein:0.3},
banana:{cal:96,protein:1.3},
idli:{cal:58,protein:2},
dosa:{cal:133,protein:3},
pizza:{cal:266,protein:11},
burger:{cal:295,protein:17},
biryani:{cal:290,protein:15},
rice:{cal:130,protein:2.7},
chapati:{cal:104,protein:3},
samosa:{cal:262,protein:6},
cake:{cal:257,protein:3},
egg:{cal:155,protein:13},
milk:{cal:42,protein:3.4},
paneer:{cal:265,protein:18},
salad:{cal:33,protein:2},
fries:{cal:312,protein:3},
noodles:{cal:138,protein:4},
pasta:{cal:131,protein:5},
chicken:{cal:239,protein:27},
fish:{cal:206,protein:22},
orange:{cal:47,protein:0.9},
grapes:{cal:69,protein:0.7},
mango:{cal:60,protein:0.8},
icecream:{cal:207,protein:3},
sandwich:{cal:250,protein:12}

};


/* FOOD ANALYSIS */

function analyzeFood(){

let file=document.getElementById("image").files[0];

if(!file)
{
alert("Please upload image");
return;
}

let name=file.name.toLowerCase();

let detected="unknown";

for(let f in foods)
{
if(name.includes(f))
{
detected=f;
break;
}
}

if(detected=="unknown")
{
document.getElementById("output").innerHTML="Food not in dataset";
return;
}

let cal=foods[detected].cal;
let protein=foods[detected].protein;

let category="";
let suggestion="";

if(cal<100)
{
category="Healthy Food";
suggestion="Good for daily diet";
}
else if(cal<250)
{
category="Moderate Food";
suggestion="Eat in balanced diet";
}
else
{
category="High Calorie Food";
suggestion="Eat in moderation";
}

document.getElementById("output").innerHTML=

"<b>Food Detected :</b> "+detected+"<br><br>"+
"<b>Calories :</b> "+cal+" kcal<br><br>"+
"<b>Protein :</b> "+protein+" g<br><br>"+
"<b>Category :</b> "+category+"<br><br>"+
"<b>Suggestion :</b> "+suggestion;

}

</script>

</body>
</html>
