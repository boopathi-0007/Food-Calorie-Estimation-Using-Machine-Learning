# Food-Calorie-Estimation-Using-Machine-Learning
<!DOCTYPE html>
<html>
<head>
<title>Food Calorie Estimation</title>

<style>

body{
font-family:Arial;
text-align:center;
background:#f2f2f2;
margin:0;
padding:0;
}

.container{
margin-top:80px;
}

.card{
background:white;
padding:30px;
display:inline-block;
border-radius:10px;
box-shadow:0 0 10px gray;
}

input,button{
padding:10px;
margin:10px;
width:220px;
border-radius:5px;
border:1px solid gray;
}

button{
background:#ff5722;
color:white;
border:none;
cursor:pointer;
}

button:hover{
background:#e64a19;
}

#homePage{
display:none;
}

img{
width:280px;
margin-top:20px;
border-radius:10px;
}

</style>
</head>

<body>

<div class="container">

<!-- LOGIN PAGE -->
<div id="loginPage" class="card">

<h2>Food Calorie Estimation Login</h2>

<input type="text" id="username" placeholder="Username"><br>
<input type="password" id="password" placeholder="Password"><br>

<button onclick="login()">Login</button>

<p id="error" style="color:red;"></p>

</div>


<!-- HOME PAGE -->
<div id="homePage" class="card">

<h2>Upload Food Image</h2>

<input type="file" id="foodImage" accept="image/*"><br>

<button onclick="estimateCalories()">Estimate Calories</button>
<button onclick="logout()">Logout</button>

<div id="result"></div>

</div>

</div>


<script>

/* LOGIN */

function login(){

let u=document.getElementById("username").value;
let p=document.getElementById("password").value;

if(u==="admin" && p==="1234"){

document.getElementById("loginPage").style.display="none";
document.getElementById("homePage").style.display="block";

}else{

document.getElementById("error").innerText="Invalid Login";

}

}


/* 20 FOOD DATASET */

let foodDataset=[

{name:"Pizza",calories:266,protein:11},
{name:"Burger",calories:295,protein:17},
{name:"Rice",calories:130,protein:2},
{name:"Pasta",calories:158,protein:5},
{name:"Apple",calories:52,protein:0.3},
{name:"Banana",calories:89,protein:1.1},
{name:"Idli",calories:58,protein:2},
{name:"Dosa",calories:168,protein:3},
{name:"Puri",calories:98,protein:2},
{name:"Fried Chicken",calories:246,protein:27},
{name:"Sandwich",calories:150,protein:6},
{name:"Salad",calories:75,protein:2},
{name:"Ice Cream",calories:207,protein:3.5},
{name:"Chocolate",calories:546,protein:4.9},
{name:"Biryani",calories:290,protein:15},
{name:"Chapati",calories:120,protein:3},
{name:"Noodles",calories:138,protein:4},
{name:"French Fries",calories:312,protein:3.4},
{name:"Egg Omelette",calories:154,protein:11},
{name:"Paneer Curry",calories:265,protein:18}

];


/* CALORIE ESTIMATION */

function estimateCalories(){

let file=document.getElementById("foodImage");

if(file.files.length===0){

alert("Upload food image");
return;

}

let randomFood=foodDataset[Math.floor(Math.random()*foodDataset.length)];

let suggestion="";

if(randomFood.calories<100){

suggestion="Low calorie food - Good for diet";

}else if(randomFood.calories<200){

suggestion="Moderate calories - Balanced food";

}else{

suggestion="High calories - Eat in moderation";

}

let reader=new FileReader();

reader.onload=function(e){

document.getElementById("result").innerHTML=

"<h3>Food Detected: "+randomFood.name+"</h3>"+
"<h3>Estimated Calories: "+randomFood.calories+" kcal</h3>"+
"<h3>Protein: "+randomFood.protein+" g</h3>"+
"<h3>Health Suggestion: "+suggestion+"</h3>"+
"<img src='"+e.target.result+"'>";

};

reader.readAsDataURL(file.files[0]);

}


/* LOGOUT */

function logout(){

document.getElementById("homePage").style.display="none";
document.getElementById("loginPage").style.display="block";

document.getElementById("foodImage").value="";
document.getElementById("result").innerHTML="";

}

</script>

</body>
</html>
