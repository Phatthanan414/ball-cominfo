<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login & Register Selection</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <!-- หน้าเลือก Login หรือ Register -->
        <div id="selection-screen" class="screen active">
            <h2>Welcome!</h2>
            <p>Choose an option to continue</p>
            <button class="btn" onclick="showScreen('login-screen')">Login</button>
            <button class="btn" onclick="showScreen('register-screen')">Register</button>
        </div>

        <!-- หน้า Login -->
        <div id="login-screen" class="screen">
            <h2>Login</h2>
            <form action="#">
                <input type="email" placeholder="Email" required>
                <input type="password" placeholder="Password" required>
                <button type="submit" class="btn">Login</button>
            </form>
            <p>Don't have an account? <a href="#" onclick="showScreen('register-screen')">Register</a></p>
            <button class="btn back" onclick="showScreen('selection-screen')">Back</button>
        </div>

        <!-- หน้า Register -->
        <div id="register-screen" class="screen">
            <h2>Register</h2>
            <form action="#">
                <input type="text" placeholder="Username" required>
                <input type="email" placeholder="Email" required>
                <input type="password" placeholder="Password" required>
                <button type="submit" class="btn">Register</button>
            </form>
            <p>Already have an account? <a href="#" onclick="showScreen('login-screen')">Login</a></p>
            <button class="btn back" onclick="showScreen('selection-screen')">Back</button>
        </div>
    </div>

    <script>
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }
    </script>

    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #f4f4f4;
        }
        .container {
            text-align: center;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .screen {
            display: none;
        }
        .screen.active {
            display: block;
        }
        .btn {
            display: block;
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            background: #3498db;
            color: white;
            cursor: pointer;
            border-radius: 5px;
        }
        .btn.back {
            background: #95a5a6;
        }
        input {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
    </style>
</body>
</html>
