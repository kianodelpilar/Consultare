<template>
  <div id="app" class="container">
    <h1>User Management</h1>
    <UserForm
      :user="selectedUser"
      :isEditing="isEditing"
      @submit="handleUserSubmit"
    />
    <div v-if="users.length" class="user-list">
      <UserCard
        v-for="user in users"
        :key="user.id"
        :user="user"
        @edit="editUser"
        @delete="deleteUser"
      />
    </div>
    <p v-else class="no-data">No users available. Please add a new user.</p>
  </div>
</template>

<script>
import UserForm from './components/UserForm.vue';
import UserCard from './components/UserCard.vue';

export default {
  components: {
    UserForm,
    UserCard
  },
  data() {
    return {
      users: [],
      selectedUser: { name: '', email: '', contactNumber: '' },
      isEditing: false
    };
  },
  methods: {
    handleUserSubmit(user) {
      // Ensure that the user data is valid (i.e., not empty and contact number is 11 digits)
      if (!user.name || !user.email || !user.contactNumber) {
        alert('Name, email, and contact number are required.');
        return;
      }

      if (!/^\d{11}$/.test(user.contactNumber)) {
        alert('Contact number must be exactly 11 digits.');
        return;
      }

      if (this.isEditing) {
        // Update existing user data
        this.users = this.users.map((u) => (u.id === user.id ? user : u));
        this.isEditing = false;
        alert('Data updated'); // Alert only for updates
      } else {
        // Add a new user
        user.id = Date.now();
        this.users.push({ ...user });
      }
      this.resetForm();
    },
    editUser(user) {
      this.selectedUser = { ...user };
      this.isEditing = true;
    },
    deleteUser(userId) {
      this.users = this.users.filter((user) => user.id !== userId);
      if (this.isEditing && this.selectedUser.id === userId) {
        this.resetForm();
      }
    },
    resetForm() {
      this.selectedUser = { name: '', email: '', contactNumber: '' };
    }
  }
};
</script>

<style>
.container {
  max-width: 800px;
  margin: auto;
  padding: 20px;
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
.user-list {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}
.no-data {
  text-align: center;
  font-size: 1.2em;
  color: #888;
}
.form-container {
  margin-bottom: 20px;
}

.form {
  display: grid;
  grid-template-columns: 1fr;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  padding: 8px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 50%;
  box-sizing: border-box;
}

.btn {
  margin-top: 10px;
  display: block;
  margin-center: auto; /* Centers the button */
}
</style>
