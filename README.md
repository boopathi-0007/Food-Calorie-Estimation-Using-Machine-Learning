<!DOCTYPE html>
<html>
<head>
<title>Food Calorie Estimation</title>

<style>

body{
margin:0;
font-family:Arial;
background:url("https://images.unsplash.com/photo-1490645935967-10de6ba17061") no-repeat center center fixed;
background-size:cover;
text-align:center;
}

.container{
margin-top:80px;
}

.card{
background:rgba(255,255,255,0.9);
padding:30px;
border-radius:12px;
display:inline-block;
box-shadow:0 0 15px black;
}

input,select,button{
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
width:260px;
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

<input type="file" id="imageUpload"><br>

<select id="foodSelect">

<option value="">Select Food</option>
<option>Pizza</option>
<option>Burger</option>
<option>Idli</option>
<option>Dosa</option>
<option>Rice</option>
<option>Biryani</option>
<option>Pasta</option>
<option>Sandwich</option>
<option>Noodles</option>
<option>Apple</option>
<option>Banana</option>
<option>IceCream</option>
<option>Chocolate</option>
<option>Salad</option>
<option>Fries</option>
<option>Omelette</option>
<option>Paneer</option>
<option>FriedChicken</option>
<option>Puri</option>
<option>Chapati</option>
<option>Soup</option>
<option>Cake</option>
<option>Donut</option>
<option>Milk</option>
<option>Cheese</option>

</select>

<br>

<button onclick="predict()">Show Calories</button>

<button onclick="logout()">Logout</button>

<br>

<img id="preview">

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


/* 25 DATASET */

const foodData={

Pizza:{cal:266,protein:11},
Burger:{cal:295,protein:17},
Idli:{cal:58,protein:2},
Dosa:{cal:168,protein:3},
Rice:{cal:130,protein:2},
Biryani:{cal:290,protein:15},
Pasta:{cal:158,protein:5},
Sandwich:{cal:150,protein:6},
Noodles:{cal:138,protein:4},
Apple:{cal:52,protein:0.3},
Banana:{cal:89,protein:1.1},
IceCream:{cal:207,protein:3.5},
Chocolate:{cal:546,protein:4.9},
Salad:{cal:75,protein:2},
Fries:{cal:312,protein:3.4},
Omelette:{cal:154,protein:11},
Paneer:{cal:265,protein:18},
FriedChicken:{cal:246,protein:27},
Puri:{cal:98,protein:2},
Chapati:{cal:120,protein:3},
Soup:{cal:90,protein:3},
Cake:{cal:257,protein:4},
Donut:{cal:452,protein:4},
Milk:{cal:103,protein:8},
Cheese:{cal:402,protein:25}

};



function predict(){

let file=document.getElementById("imageUpload").files[0];
let food=document.getElementById("foodSelect").value;

if(!file || !food){

alert("Upload image and select food");

return;

}

let img=document.getElementById("preview");

img.src=URL.createObjectURL(file);

let cal=foodData[food].cal;
let protein=foodData[food].protein;

let suggestion="";

if(cal<100){

suggestion="Low calorie food";

}else if(cal<200){

suggestion="Moderate calories";

}else{

suggestion="High calories";

}

document.getElementById("result").innerHTML=

"<h3>Food: "+food+"</h3>"+
"<h3>Calories: "+cal+" kcal</h3>"+
"<h3>Protein: "+protein+" g</h3>"+
"<h3>Health Suggestion: "+suggestion+"</h3>";

}



/* LOGOUT */

function logout(){

document.getElementById("homePage").style.display="none";
document.getElementById("loginPage").style.display="block";

}

</script>

</body>
</html>
