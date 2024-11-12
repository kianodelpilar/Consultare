<template>
  <div class="user-card">
    <p><strong>Name:</strong> {{ user.name }}</p>
    <p><strong>Email:</strong> {{ user.email }}</p>
    <p><strong>Contact Number:</strong> {{ user.contactNumber }}</p>
    <div class="card-actions">
      <button class="btn btn-warning" @click="$emit('edit', user)">Edit</button>
      <button class="btn btn-danger" @click="$emit('delete', user.id)">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['user']
};
</script>

<style scoped>
.user-card {
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 350px;
}
.card-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}
.btn {
  cursor: pointer;
}
</style>
