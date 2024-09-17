<template>
    <div class="signup-container">
        <form @submit.prevent="handleSignUp" class="signup-form">
            <h2>Create an Account</h2>

            <label>Email</label>
            <input v-model="email" type="email" placeholder="Enter your email" required class="input-field" />

            <label>Password</label>
            <input v-model="password" type="password" placeholder="Enter your password" required class="input-field" />

            <label>Confirm Password</label>
            <input v-model="confirmPassword" type="password" placeholder="Confirm your password" required
                class="input-field" />

            <button type="submit" class="submit-btn">Sign Up</button>
            <div class="login-link">
                <p>Already have an account? <router-link to="/login">Log In</router-link></p>
            </div>
            <div class="social-login">
                <p>Or continue with</p>
                <div class="social-buttons">
                    <button class="google-btn" @click="signUpWithGoogle">Google</button>
                </div>
            </div>
        </form>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            confirmPassword: '',
        };
    },
    methods: {
        handleSignUp() {
            // Check if the password is at least 8 characters long
            if (this.password.length < 8) {
                alert('Password must be at least 8 characters.');
                return;
            }
            // Check if password and confirm password match
            if (this.password !== this.confirmPassword) {
                alert('Passwords do not match');
                return;
            }

            // Create a new user object
            const newUser = {
                email: this.email,
                password: this.password,
            };

            // Retrieve existing users from localStorage
            const storedUsers = JSON.parse(localStorage.getItem('users')) || [];

            // Check if the user already exists based on email
            const userExists = storedUsers.find(user => user.email === this.email);
            if (userExists) {
                alert('A user with this email already exists.');
                return;
            }

            // Add the new user to the array of users
            storedUsers.push(newUser);

            // Save the updated users array back to localStorage
            localStorage.setItem('users', JSON.stringify(storedUsers));

            alert('Account created successfully!');
            this.$router.push('/login');
        },
        signUpWithGoogle() {
            alert('Google Sign Up Coming Soon!');
        }
    },
};
</script>

  
<style scoped>

.signup-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 20px;
    background: linear-gradient(to right, rgba(13, 19, 32, 0.9), rgba(51, 64, 79, 0.7)), 
    url('https://images.unsplash.com/photo-1483982258113-b72862e6cff6?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fGRhcmt8ZW58MHx8MHx8fDA%3D');
    background-size: cover;
    background-position: center right;
    animation: gradient-animation 5s ease infinite;
}

/* Form Styles */
.signup-form {
    background-color: #1D263A;  /* Same dark background color as the login form */
    padding: 40px;
    border-radius: 15px;
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
    max-width: 450px;
    width: 100%;
    text-align: center;
    color: white;  /* Ensures the text color matches the dark background */
    animation: slide-down 1s ease forwards;
}
h2 {
    font-size: 28px;
    margin-bottom: 20px;
    font-weight: 700;
    color: white;  /* Same text color as the login page */
}

/* Input Styles */
.input-field {
    width: 100%;
    padding: 12px;
    margin-top: 10px;
    margin-bottom: 20px;
    border-radius: 8px;
    border: 1px solid #3C4B64;
    font-size: 14px;
    background-color: #2A3449;
    color: white;  /* White input text for consistency */
    outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
}

.input-field:focus {
    border-color: #4F93E3;
    box-shadow: 0 4px 8px rgba(79, 147, 227, 0.2);
}

/* Button with hover animation */
.submit-btn {
    width: 100%;
    background: linear-gradient(45deg, #4A9DFF, #5D6CC3);
    color: white;
    border: none;
    padding: 12px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    transition: background 0.3s ease, transform 0.3s ease;
    margin-bottom: 10px;
}

.submit-btn:hover {
    background: linear-gradient(45deg, #669EFF, #798BC8);
    transform: translateY(-3px);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

/* Social Login Button */
.social-buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100px;
    margin: 10px auto;
}

.google-btn {
    flex: 1;
    padding: 10px;
    border-radius: 8px;
    background-color: #DB4437;
    color: white;
    border: none;
    cursor: pointer;
    transition: background 0.3s ease;
}

.google-btn:hover {
    background-color: #C13525;
    transform: translateY(-3px);
}

/* Login link style */
.login-link p a{
    color: #4F93E3;
    text-decoration: none; 
}

/* Animation for smooth form appearance */
@keyframes slide-down {
    0% {
        opacity: 0;
        transform: translateY(-20px);
    }

    100% {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
  