<template>
  <div class="dashboard-container">
    <!-- Logout Button at the top-right corner -->
    <div class="header">
      <h1>Welcome to the Dashboard</h1>
    </div>
    <button @click="logout" class="logout-button">
      <i class="fas fa-sign-out-alt"></i>
    </button>
    <div class="navigation-links">
      <router-link to="/dashboard" class="nav-link">View Dashboard</router-link>
      <router-link to="/userdata" class="nav-link">Go to Other Page</router-link>
    </div>
    

    <!-- Flex container to display components side by side -->
    <div class="components-container">
      <div class="component-left">
        <User :users="users" @add-user="addUser"></User>
      </div>
      <div class="component-right">
        <Form></Form>
      </div>
    </div>
  </div>
</template>

<script>
import User from './User_Details.vue';
import Form from './Form_details.vue';
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'UserDashboard',
  methods: {
    ...mapActions(['addUser']),
    logout() {
      localStorage.removeItem('authUser');
      this.$router.push('/login');
    }
  },
  computed: {
    ...mapGetters(['allUsers']),
    users() {
      return this.allUsers;
    }
  },
  components: {
    User,
    Form
  }
};
</script>

<style scoped>
.dashboard-container {
  position: relative; 
  display: flex;
  flex-direction: column;
  background-color: #7d8c92;
  justify-content: center;
  overflow-y: hidden;
  height: 100vh;
}

.logout-button {
  position: absolute;
  top: 20px; 
  right: 20px; 
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 1.5em;
  color: #ff6347;
}

.logout-button i {
  font-size: 1.5em;
}

.header {
  text-align: center;
  color: aliceblue;
}

.header h1 {
  position: absolute;
  top: 20px;
  margin-left: 35%;
  font-size: 2.5em;
}


.components-container {
  display: flex;
  justify-content: space-between;
  width: 100%; 
  padding: 20px;
  box-sizing: border-box;
  margin-top: 20px;
}


.component-left {
  width: 48%; 
}

.component-right {
  width: 48%;
}
.navigation-links {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}

.nav-link {
  margin: 0 15px;
  font-size: 1.1em;
  color: #090909;
  text-decoration: none;
  padding: 12px 25px;
  border-radius: 8px;
  background-color: #9fe7f3;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.nav-link:hover {
  background-color: #4ac8e7;
  transform: translateY(-2px);
}

.nav-link:active {
  background-color: #003d7a;
  transform: translateY(0);
}

</style>
