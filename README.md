# Food-Calorie-Estimation-Using-Machine-Learning
from flask import Flask, request, redirect, url_for, render_template_string
import numpy as np
from sklearn.linear_model import LinearRegression
import os

app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = 'uploads'

# Create uploads folder automatically
if not os.path.exists('uploads'):
    os.makedirs('uploads')

# ------------------------
# Create Simple ML Model
# ------------------------
X = np.array([[1000], [2000], [3000], [4000], [5000]])
y = np.array([150, 250, 350, 450, 550])

model = LinearRegression()
model.fit(X, y)

# ------------------------
# Simple Login Credentials
# ------------------------
USERNAME = "admin"
PASSWORD = "1234"

# ------------------------
# Login Page
# ------------------------
@app.route('/')
def login():
    return render_template_string('''
        <h2>Food Calorie Estimation - Login</h2>
        <form method="POST" action="/login">
            <input type="text" name="username" placeholder="Username" required><br><br>
            <input type="password" name="password" placeholder="Password" required><br><br>
            <button type="submit">Login</button>
        </form>
    ''')

@app.route('/login', methods=['POST'])
def login_check():
    username = request.form['username']
    password = request.form['password']

    if username == USERNAME and password == PASSWORD:
        return redirect('/home')
    else:
        return "<h3>Invalid Login</h3><a href='/'>Try Again</a>"

# ------------------------
# Home Page - Upload Image
# ------------------------
@app.route('/home')
def home():
    return render_template_string('''
        <h2>Upload Food Image</h2>
        <form method="POST" action="/predict" enctype="multipart/form-data">
            <input type="file" name="image" required><br><br>
            <button type="submit">Estimate Calories</button>
        </form>
    ''')

# ------------------------
# Prediction
# ------------------------
@app.route('/predict', methods=['POST'])
def predict():
    file = request.files['image']

    if file:
        filepath = os.path.join(app.config['UPLOAD_FOLDER'], file.filename)
        file.save(filepath)

        # Use file size as dummy ML input
        size = os.path.getsize(filepath)
        size = np.array([[size]])

        prediction = model.predict(size)
        calories = round(prediction[0], 2)

        return render_template_string(f'''
            <h2>Calorie Estimation Result</h2>
            <img src="/{filepath}" width="300"><br><br>
            <h3>Estimated Calories: {calories} kcal</h3>
            <a href="/home">Try Another</a>
        ''')

    return "No file uploaded"

# ------------------------
# Run App
# ------------------------
if __name__ == "__main__":
    app.run(debug=True)
