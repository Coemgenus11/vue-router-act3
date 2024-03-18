<template>
    <div class="container mt-5">
      <div class="row justify-content-center">
        <div class="col-md-6">
          <div v-if="!isLoggedIn" class="card">
            <div class="card-header">
              <h1 class="card-title">Login</h1>
            </div>
            <div class="card-body">
              <form @submit.prevent="login">
                <div class="mb-3">
                  <label for="username" class="form-label">Username:</label>
                  <input type="text" id="username" v-model="username" class="form-control">
                </div>
                <div class="mb-3">
                  <label for="password" class="form-label">Password:</label>
                  <input type="password" id="password" v-model="password" class="form-control">
                </div>
                <button type="submit" class="btn btn-primary">Login</button>
              </form>
            </div>
          </div>
          <div v-else class="card">
            <div class="card-body">
              <p>You are already logged in.</p>
              <router-link to="/shopping" class="btn btn-primary">Go to Shop</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  

<script>
export default {
    data() {
        return {
            username: '',
            password: ''
        };
    },
    computed: {
        isLoggedIn() {
            return localStorage.getItem('token') !== null;
        }
    },
    methods: {
        login() {
            if (this.username === 'username' && this.password === 'password123') {
                // Authentication successful
                localStorage.setItem('token', '12345');
                this.$router.push({ name: 'shopping' });
            } else {
                // Authentication failed
                alert('Invalid username or password');
            }
        }
    }
};
</script>
