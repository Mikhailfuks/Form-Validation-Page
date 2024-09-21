<!DOCTYPE html>
<html>
<head>
  <title>Form Validation</title>
  <style>
    .error {
      color: red;
    }
  </style>
</head>
<body>
  <h1>Form Validation</h1>

  <form id="myForm" onsubmit="return validateForm()">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required><span class="error" id="nameError"></span><br><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required><span class="error" id="emailError"></span><br><br>

    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required><span class="error" id="passwordError"></span><br><br>

    <label for="confirm-password">Confirm Password:</label>
    <input type="password" id="confirm-password" name="confirm-password" required><span class="error" id="confirmPasswordError"></span><br><br>

    <input type="submit" value="Submit">
  </form>

  <script src="script.js"></script>
</body>
</html>



function validateForm() {
  let name = document.getElementById("name").value;
  let email = document.getElementById("email").value;
  let password = document.getElementById("password").value;
  let confirmPassword = document.getElementById("confirm-password").value;

  let nameError = document.getElementById("nameError");
  let emailError = document.getElementById("emailError");
  let passwordError = document.getElementById("passwordError");
  let confirmPasswordError = document.getElementById("confirmPasswordError");

  // Name Validation
  if (name === "") {
    nameError.textContent = "Name is required";
    return false;
  } else {
    nameError.textContent = ""; 
  }

  // Email Validation
  if (email === "") {
    emailError.textContent = "Email is required";
    return false;
  } else if (!validateEmail(email)) {
    emailError.textContent = "Invalid email format";
    return false;
  } else {
    emailError.textContent = ""; 
  }

  // Password Validation
  if (password === "") {
    passwordError.textContent = "Password is required";
    return false;
  } else if (password.length < 8) {
    passwordError.textContent = "Password must be at least 8 characters";
    return false;
  } else {
    passwordError.textContent = ""; 
  }

  // Confirm Password Validation
  if (confirmPassword === "") {
    confirmPasswordError.textContent = "Confirm password is required";
    return false;
  } else if (confirmPassword !== password) {
    confirmPasswordError.textContent = "Passwords do not match";
    return false;
  } else {
    confirmPasswordError.textContent = ""; 
  }

  // If all validations pass, return true to submit the form
  return true;
}

// Helper function for email validation
function validateEmail(email) {
  const re = /^[^s@]+@[^s@]+.[^s@]+$/;
  return re.test(email);
}
