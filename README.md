<!DOCTYPE html>
<html>
<head>

<title>Indian Food Nutrition Analyzer</title>

<style>

body{
font-family:Arial;
text-align:center;
background:#f5f5f5;
}

h1{
margin-top:40px;
}

input{
padding:10px;
width:240px;
}

button{
padding:10px 20px;
background:green;
color:white;
border:none;
margin-top:10px;
font-size:16px;
}

img{
width:300px;
border-radius:10px;
margin-top:20px;
}

#result{
margin-top:20px;
font-size:18px;
}

</style>

</head>

<body>

<h1>Indian Food Nutrition Analyzer</h1>

<input type="text" id="foodName" placeholder="Example: dosa">

<br><br>

<button onclick="analyze()">Analyze</button>

<div id="result"></div>

<script>

let foods={

idli:{cal:58,protein:2,img:"https://upload.wikimedia.org/wikipedia/commons/3/3f/Idli_Sambar.jpg"},
dosa:{cal:133,protein:3,img:"https://upload.wikimedia.org/wikipedia/commons/5/5f/Masala_Dosa.jpg"},
rasam:{cal:60,protein:2,img:"https://upload.wikimedia.org/wikipedia/commons/4/4d/Rasam.jpg"},
sambar:{cal:90,protein:5,img:"https://upload.wikimedia.org/wikipedia/commons/2/2f/Sambar.jpg"},
pongal:{cal:180,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/e/e3/Ven_Pongal.jpg"},
upma:{cal:120,protein:3,img:"https://upload.wikimedia.org/wikipedia/commons/8/8f/Upma.jpg"},
vada:{cal:150,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/7/7b/Vada.jpg"},
poha:{cal:180,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/5/55/Poha.jpg"},
chapati:{cal:104,protein:3,img:"https://upload.wikimedia.org/wikipedia/commons/0/0b/Chapati.jpg"},
naan:{cal:260,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/9/9c/Naan.jpg"},

parotta:{cal:300,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/4/49/Parotta.jpg"},
poori:{cal:250,protein:5,img:"https://upload.wikimedia.org/wikipedia/commons/8/8d/Poori.jpg"},
veg_biryani:{cal:250,protein:7,img:"https://upload.wikimedia.org/wikipedia/commons/0/0b/Vegetable_Biryani.jpg"},
chicken_biryani:{cal:290,protein:15,img:"https://upload.wikimedia.org/wikipedia/commons/3/3e/Chicken_Biryani.jpg"},
mutton_biryani:{cal:320,protein:18,img:"https://upload.wikimedia.org/wikipedia/commons/7/7c/Mutton_Biryani.jpg"},
pulao:{cal:220,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/3/35/Pulao.jpg"},
lemon_rice:{cal:200,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/7/7f/Lemon_rice.jpg"},
curd_rice:{cal:180,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/4/45/Curd_Rice.jpg"},
tamarind_rice:{cal:210,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/4/4f/Puliyodarai.jpg"},
rajma:{cal:240,protein:9,img:"https://upload.wikimedia.org/wikipedia/commons/3/3d/Rajma_Chawal.jpg"},

dal_tadka:{cal:180,protein:8,img:"https://upload.wikimedia.org/wikipedia/commons/4/4c/Dal_Tadka.jpg"},
dal_makhani:{cal:300,protein:10,img:"https://upload.wikimedia.org/wikipedia/commons/6/6c/Dal_Makhani.jpg"},
palak_paneer:{cal:280,protein:11,img:"https://upload.wikimedia.org/wikipedia/commons/a/a1/Palak_Paneer.jpg"},
paneer_butter_masala:{cal:300,protein:10,img:"https://upload.wikimedia.org/wikipedia/commons/4/4f/Paneer_Butter_Masala.jpg"},
aloo_paratha:{cal:260,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/6/6a/Aloo_Paratha.jpg"},
gobi_paratha:{cal:240,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/0/0e/Gobi_Paratha.jpg"},
paneer_paratha:{cal:280,protein:9,img:"https://upload.wikimedia.org/wikipedia/commons/3/3e/Paneer_Paratha.jpg"},
veg_samosa:{cal:262,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/3/3b/Samosa.jpg"},
pakora:{cal:220,protein:5,img:"https://upload.wikimedia.org/wikipedia/commons/4/4f/Pakora.jpg"},
pav_bhaji:{cal:400,protein:10,img:"https://upload.wikimedia.org/wikipedia/commons/7/7f/Pav_Bhaji.jpg"},

vada_pav:{cal:300,protein:8,img:"https://upload.wikimedia.org/wikipedia/commons/2/2a/Vada_Pav.jpg"},
misal_pav:{cal:350,protein:12,img:"https://upload.wikimedia.org/wikipedia/commons/3/3f/Misal_Pav.jpg"},
dhokla:{cal:160,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/5/5b/Dhokla.jpg"},
thepla:{cal:200,protein:5,img:"https://upload.wikimedia.org/wikipedia/commons/e/e2/Thepla.jpg"},
khichdi:{cal:180,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/4/49/Khichdi.jpg"},
jalebi:{cal:300,protein:2,img:"https://upload.wikimedia.org/wikipedia/commons/6/6f/Jalebi.jpg"},
gulab_jamun:{cal:350,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/4/4e/Gulab_Jamun.jpg"},
rasgulla:{cal:186,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/0/0d/Rasgulla.jpg"},
kheer:{cal:250,protein:6,img:"https://upload.wikimedia.org/wikipedia/commons/3/3a/Kheer.jpg"},
laddu:{cal:280,protein:5,img:"https://upload.wikimedia.org/wikipedia/commons/5/5c/Laddu.jpg"},

mysore_pak:{cal:300,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/6/63/Mysore_Pak.jpg"},
halwa:{cal:290,protein:4,img:"https://upload.wikimedia.org/wikipedia/commons/4/4f/Halwa.jpg"},
chole_bhature:{cal:350,protein:12,img:"https://upload.wikimedia.org/wikipedia/commons/8/89/Chole_Bhature.jpg"},
butter_chicken:{cal:300,protein:20,img:"https://upload.wikimedia.org/wikipedia/commons/7/7e/Butter_Chicken.jpg"},
tandoori_chicken:{cal:220,protein:25,img:"https://upload.wikimedia.org/wikipedia/commons/3/3c/Tandoori_Chicken.jpg"},
fish_curry:{cal:200,protein:22,img:"https://upload.wikimedia.org/wikipedia/commons/4/
