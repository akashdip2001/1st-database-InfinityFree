# 1st-database
1st database for freecad app

# index.php

```php
<?php
session_start();
require_once 'functions.php';
if (isset($_SESSION['user_id'])) {
    if (checkPaymentStatus($_SESSION['user_id'])) {
        header("Location: next.php");
        exit();
    }
}
header("Location: login.php");
exit();
?>
```
# login.php

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <link rel="stylesheet" type="text/css" href="styles.css">

    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h2 {
            text-align: center;
            color: #333;
        }

        form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        label {
            margin-bottom: 8px;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
        }

        input[type="submit"] {
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }

        input[type="submit"]:hover {
            background-color: #0056b3;
        }

        .error-message {
            color: #ff0000;
            text-align: center;
            margin-top: 10px;
        }

        .signup-link {
            text-align: center;
            margin-top: 20px;
        }

        .signup-link a {
            color: #007bff;
            text-decoration: none;
        }

        .signup-link a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Login</h2>
        <form method="POST" action="">
            <div>
                <label>Email:</label>
                <input type="email" name="email" required>
            </div>
            <div>
                <label>Password:</label>
                <input type="password" name="password" required>
            </div>
            <div>
                <input type="submit" value="Login">
            </div>
        </form>
        <?php
            // Display error messages if any
            if (isset($_SESSION['login_error'])) {
                echo '<div class="error-message">' . $_SESSION['login_error'] . '</div>';
                unset($_SESSION['login_error']);
            }
        ?>
        <div class="signup-link">
            <p>Don't have an account? <a href="signup.php">Sign up here</a>.</p>
        </div>
    </div>
</body>
</html>
```

# signup.php

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sign Up</title>
    <link rel="stylesheet" type="text/css" href="styles.css">

    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h2 {
            text-align: center;
            color: #333;
        }

        form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        label {
            margin-bottom: 8px;
        }

        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
        }

        input[type="submit"] {
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }

        input[type="submit"]:hover {
            background-color: #0056b3;
        }

        .error-message {
            color: #ff0000;
            text-align: center;
            margin-top: 10px;
        }

        .signup-link {
            text-align: center;
            margin-top: 20px;
        }

        .signup-link a {
            color: #007bff;
            text-decoration: none;
        }

        .signup-link a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Sign Up</h2>
        <form method="POST" action="">
            <div>
                <label>Name:</label>
                <input type="text" name="name" required>
            </div>
            <div>
                <label>College Name:</label>
                <input type="text" name="college" required>
            </div>
            <div>
                <label>Email:</label>
                <input type="email" name="email" required>
            </div>
            <div>
                <label>Mobile:</label>
                <input type="text" name="mobile" required>
            </div>
            <div>
                <label>Password:</label>
                <input type="password" name="password" required>
            </div>
            <div>
                <input type="submit" value="Sign Up">
            </div>
        </form>
        <?php
            // Display error messages if any
            if (isset($_SESSION['signup_error'])) {
                echo '<div class="error-message">' . $_SESSION['signup_error'] . '</div>';
                unset($_SESSION['signup_error']);
            }
        ?>
        <div class="signup-link">
            <p>Already have an account? <a href="login.php">Login here</a>.</p>
        </div>
    </div>
</body>
</html>
```

# enter_otp.php

```php
<?php
session_start();
require_once 'functions.php';
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $enteredOTP = $_POST['otp'];
    $storedOTP = $_SESSION['otp'];
    if ($enteredOTP == $storedOTP) {
        // OTP matched, email and mobile are verified
        // Perform necessary actions (e.g., register user, update database, etc.)
        // Redirect to a success page
        header("Location: success.php");
        exit();
    } else {
        // OTP did not match, show error message
        echo "<script>alert('Invalid OTP. Please try again.');</script>";
    }
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>OTP Verification</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
    <!-- Add your CSS styles here -->
</head>
<body>
    <div class="container">
        <h2>OTP Verification</h2>
        <form method="POST" action="">
            <div>
                <label>Enter OTP:</label>
                <input type="text" name="otp" required>
            </div>
            <div>
                <input type="submit" value="Verify OTP">
            </div>
        </form>
    </div>
</body>
</html>
```

# verify.php

```php
<?php
session_start();
require_once 'functions.php';
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $email = $_POST['email'];
    $mobile = $_POST['mobile'];
    $otp = generateOTP();
    // Save the OTP in the session for verification
    $_SESSION['otp'] = $otp;
    // Send the OTP to the user's email and mobile number
    sendOTP($email, $mobile, $otp);
    // Redirect to the OTP verification page
    header("Location: enter_otp.php");
    exit();
}
?>
```

# functions.php

```php
<?php
// Add your database connection details here
$host = "your_database_host";
$username = "your_database_username";
$password = "your_database_password";
$database = "verification_app";

$conn = mysqli_connect($host, $username, $password, $database);

if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

function generateOTP() {
    return rand(100000, 999999); // Generate a 6-digit OTP
}

function sendOTP($email, $mobile, $otp) {
    // Implement your code to send OTP (email and SMS)
}

function saveUser($name, $college, $email, $mobile, $password) {
    global $conn;
    $otp = generateOTP();
    $hashedPassword = password_hash($password, PASSWORD_DEFAULT);

    $sql = "INSERT INTO users (name, college, email, mobile, password, otp) 
            VALUES ('$name', '$college', '$email', '$mobile', '$hashedPassword', $otp)";

    return mysqli_query($conn, $sql);
}

// Add other necessary functions
?>
```

# styles.css

```css
/* styles.css */

body {
    font-family: Arial, sans-serif;
}

.container {
    width: 50%;
    margin: 50px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

form {
    margin-top: 20px;
}

label {
    display: block;
    margin-bottom: 5px;
}

input {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
}

input[type="submit"] {
    background-color: #4caf50;
    color: white;
    cursor: pointer;
}

input[type="submit"]:hover {
    background-color: #45a049;
}
```
