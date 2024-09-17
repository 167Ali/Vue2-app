<template>
  <div class="form-container">
    <div class="form-header">
      <h2>User Form</h2>
      <p>Please Enter Your Details </p>
    </div>

    <form @submit.prevent="submitForm" class="form">
      <div class="form-group">
        <div class="input-icon">
          <i class="fas fa-user"></i>
          <input v-model="name" type="text" placeholder="First name" required class="form-input">
        </div>
      </div>
      <div class="form-group">
        <div class="input-icon">
          <i class="fas fa-user"></i>
          <input v-model="lastName" type="text" placeholder="Last name" required class="form-input">
        </div>
      </div>
      <div class="form-group">
        <div class="input-icon">
          <i class="fas fa-envelope"></i>
          <input v-model="email" type="email" placeholder="Email" required class="form-input">
        </div>
      </div>
      <div class="form-buttons">
        <button type="submit" class="submit-class">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import { mapActions } from 'vuex';
export default {
  data() {
    return {
      name: '',
      lastName: '',
      email: ''
    };
  },
  methods: {
    ...mapActions(['addUser']),
    submitForm() {
      const user = {
        name: this.name,
        lastName: this.lastName,
        email: this.email,
      };
      this.addUser(user);
      this.resetForm();
    },
      resetForm() {
      this.name = '';
      this.lastName = '';
      this.email = '';
    }
  }
};
</script>

<style scoped>
.form-container {
  background-color: #1e1f29;
  color: #ffffff;
  padding: 40px;
  max-width: 450px;
  margin:auto;
  border-radius: 20px;
  box-shadow: 0px 8px 30px rgba(0, 0, 0, 0.2);
  font-family: 'Roboto', sans-serif;
}

.form-header h2 {
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 10px;
}

.form-header p {
  font-size: 1em;
  color: #a9a9a9;
  margin-bottom: 10px;
}


.form-group {
  margin-bottom: 20px;
}

.input-icon {
  position: relative;
  display: flex;
  align-items: center;
}

.input-icon i {
  position: absolute;
  left: 15px;
  color: #a9a9a9;
}

.form-input {
  width: 100%;
  padding: 15px 50px;
  border-radius: 10px;
  border: none;
  background-color: #2b2e3c;
  color: white;
  font-size: 1em;
  outline: none;
}

.form-input::placeholder {
  color: #a9a9a9;
}

.form-buttons {
  display: flex;
  justify-content: center;
}

button {
  padding: 12px 25px;
  border-radius: 10px;
  border: none;
  font-size: 1em;
  cursor: pointer;
}

.submit-class {
  background-color: #4d8ef7;
  color: white;
  transition: background-color 0.3s ease;
}

.submit-class:hover {
  background-color: #5a9bff;
}
</style>
