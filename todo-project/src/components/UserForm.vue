<template>
  <div class="form-container">
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input v-model="user.name" id="name" placeholder="Name" required />
      </div>
      <div class="form-group">
        <label for="email">Email</label>
        <input v-model="user.email" id="email" type="email" placeholder="Email" required />
      </div>
      <div class="form-group">
        <label for="contactNumber">Contact Number</label>
        <input v-model="user.contactNumber" id="contactNumber" placeholder="Contact Number" maxlength="11" required />
      </div>
      <button class="btn btn-primary" type="submit">
        {{ isEditing ? 'Update User' : 'Add User' }}
      </button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['user', 'isEditing'],
  methods: {
    handleSubmit() {
      this.$emit('submit', { ...this.user });
    }
  }
};
</script>

<style scoped>
.form-container {
  margin-bottom: 20px;
}
.form-group {
  margin-bottom: 10px;
}
.btn {
  margin-top: 10px;
}
</style>
