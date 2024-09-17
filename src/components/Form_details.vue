<template>
  <div class="form-container">
    <h2>All Users</h2>
    <div v-if="users.length === 0" class="no-users">
      No users found.
    </div>
    <div v-else class="users-list">
      <div v-for="(user, index) in users" :key="index" class="user-card">
        <div class="user-details">
          <!-- Avatar Section -->
          <div class="user-avatar">
            <i class="fas fa-user-circle"></i>
          </div>
          <!-- User Information -->
          <div class="user-info">
            <h3>{{ user.name }} {{ user.lastName }}</h3>
            <p class="user-email">{{ user.email }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
export default {
  computed: {
    ...mapGetters(['allUsers']),
    users() {
      return this.allUsers;
    }
  }
};
</script>

<style scoped>
.form-container {
  padding: 40px;
  background-color: #1e1f29;
  color: #ffffff;
  max-width: 450px;
  height: 530px;
  margin: 0 auto;   
  border-radius: 15px;
  box-shadow: 0px 8px 30px rgba(0, 0, 0, 0.3);
  font-family: 'Roboto', sans-serif;
  overflow-y: auto;
}

h2 {
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 20px;
  text-align: center;
}

.no-users {
  text-align: center;
  font-size: 1.2em;
  color: #a9a9a9;
}

.users-list {
  display: flex;
  flex-direction: column;
}

/* Adjust the layout and width of user cards */
.user-card {
  background-color: #2b2e3c;
  padding: 20px;
  margin-bottom: 15px;
  border-radius: 10px;
  width: 100%;
  display: flex;
  align-items: center;
  box-shadow: 0px 5px 20px rgba(0, 0, 0, 0.1);

}

/* Flexbox for avatar and user info alignment */
.user-details {
  display: flex;
  align-items: center;
  width: 100%; /* Ensures the content takes the full width of the card */
}

/* Avatar styling */
.user-avatar {
  margin-right: 20px;
}

.user-avatar i {
  font-size: 50px;
  color: #4CAF50;
}

/* User info (name and email) */
.user-info h3 {
  font-size: 1.2em;
  margin: 0;
  color: #ffffff;
  
}

.user-info .user-email {
  font-size: 1em;
  color: #a9a9a9;
  margin-top: 5px;
  margin-bottom: 5px;
}
</style>
