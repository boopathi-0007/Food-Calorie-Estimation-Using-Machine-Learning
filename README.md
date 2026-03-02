# Food-Calorie-Estimation-Using-Machine-Learning
<!DOCTYPE html>
<html>
<head>
    <title>Food Calorie Estimation - ML Project</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;

            /* Background Image */
            background: url('https://images.unsplash.com/photo-1490645935967-10de6ba17061') no-repeat center center fixed;
            background-size: cover;
        }

        .container {
            margin-top: 80px;
        }

        .card {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            display: inline-block;
            border-radius: 15px;
            box-shadow: 0 0 15px black;
        }

        input, button {
            padding: 10px;
            margin: 10px;
            width: 200px;
            border-radius: 5px;
            border: 1px solid gray;
        }

        button {
            background-color: #ff5722;
            color: white;
            border: none;
            cursor: pointer;
        }

        button:hover {
            background-color: #e64a19;
        }

        #homePage {
            display: none;
        }

        img {
            margin-top: 20px;
            width: 300px;
            border-radius: 10px;
        }

        h2 {
            color: #333;
        }
    </style>
</head>
<body>

<div class="container">

    <!-- LOGIN PAGE -->
    <div id="loginPage" class="card">
        <h2>Food Calorie Estimation - Login</h2>

        <form onsubmit="login(event)">
            <input type="text" id="username" placeholder="Username" required><br>
            <input type="password" id="password" placeholder="Password" required><br>
            <button type="submit">Login</button>
        </form>

        <p id="loginError" style="color:red;"></p>
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
    const correctUsername = "admin";
    const correctPassword = "1234";

    function login(event) {
        event.preventDefault();

        let user = document.getElementById("username").value.trim();
        let pass = document.getElementById("password").value.trim();

        if (user === correctUsername && pass === correctPassword) {
            document.getElementById("loginPage").style.display = "none";
            document.getElementById("homePage").style.display = "block";
            document.getElementById("loginError").innerText = "";
        } else {
            document.getElementById("loginError").innerText = "Invalid Username or Password";
        }
    }

    function estimateCalories() {
        let fileInput = document.getElementById("foodImage");
        let resultDiv = document.getElementById("result");

        resultDiv.innerHTML = "";

        if (fileInput.files.length === 0) {
            alert("Please upload an image");
            return;
        }

        let file = fileInput.files[0];

        if (!file.type.startsWith("image/")) {
            alert("Please upload a valid image file");
            return;
        }

        let fileSize = file.size;
        let calories = (fileSize / 1000).toFixed(2);

        let reader = new FileReader();
        reader.onload = function(e) {
            resultDiv.innerHTML = `
                <h3>Estimated Calories: ${calories} kcal</h3>
                <img src="${e.target.result}">
            `;
        };

        reader.readAsDataURL(file);
    }

    function logout() {
        document.getElementById("homePage").style.display = "none";
        document.getElementById("loginPage").style.display = "block";
        document.getElementById("foodImage").value = "";
        document.getElementById("result").innerHTML = "";
    }
</script>

</body>
</html>
