# Food-Calorie-Estimation-Using-Machine-Learning
<!DOCTYPE html>
<html>
<head>
    <title>Food Calorie Estimation - ML Project</title>
    <style>
        body {
            font-family: Arial;
            text-align: center;
            background-color: #f4f4f4;
        }

        .container {
            margin-top: 50px;
            padding: 20px;
        }

        input, button {
            padding: 10px;
            margin: 10px;
        }

        #homePage {
            display: none;
        }

        img {
            margin-top: 20px;
            width: 300px;
        }
    </style>
</head>
<body>

<div class="container">

    <!-- LOGIN PAGE -->
    <div id="loginPage">
        <h2>Food Calorie Estimation - Login</h2>
        <input type="text" id="username" placeholder="Username"><br>
        <input type="password" id="password" placeholder="Password"><br>
        <button onclick="login()">Login</button>
        <p id="loginError" style="color:red;"></p>
    </div>

    <!-- HOME PAGE -->
    <div id="homePage">
        <h2>Upload Food Image</h2>
        <input type="file" id="foodImage" accept="image/*"><br>
        <button onclick="estimateCalories()">Estimate Calories</button>

        <div id="result"></div>
    </div>

</div>

<script>
    // Simple login credentials
    const correctUsername = "admin";
    const correctPassword = "1234";

    function login() {
        let user = document.getElementById("username").value;
        let pass = document.getElementById("password").value;

        if (user === correctUsername && pass === correctPassword) {
            document.getElementById("loginPage").style.display = "none";
            document.getElementById("homePage").style.display = "block";
        } else {
            document.getElementById("loginError").innerText = "Invalid Username or Password";
        }
    }

    function estimateCalories() {
        let fileInput = document.getElementById("foodImage");
        let resultDiv = document.getElementById("result");

        if (fileInput.files.length === 0) {
            alert("Please upload an image");
            return;
        }

        let file = fileInput.files[0];

        // Dummy ML Logic (Using file size)
        let fileSize = file.size;  

        // Simple Linear Formula (Simulated ML Model)
        let calories = (fileSize / 10).toFixed(2);

        let reader = new FileReader();
        reader.onload = function(e) {
            resultDiv.innerHTML = `
                <h3>Estimated Calories: ${calories} kcal</h3>
                <img src="${e.target.result}">
            `;
        }

        reader.readAsDataURL(file);
    }
</script>

</body>
</html>
