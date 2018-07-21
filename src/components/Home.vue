<template>
  <div class="home">
    <div class="form-container" v-show="showForm">
      <h1>Join the Web Developers Club!</h1>
      <p>Sign up to access our special, secret page. Just create an account and answer a brief survey.</p>

      <form v-on:submit.prevent="validateForm">
        <div class="error" v-show="showError">
          <p v-if="errors.length"> Invalid Information. Please correct the following: </p>
          <ul>
            <li v-for="error in errors"> {{ error }} </li>
          </ul>        
        </div>
        <p>
            <label for="username">Username</label>
                <input type="text" id="username" v-model="username">
        </p>
        <p>
            <label for="email">Email</label> 
                <input type="email" id="email" v-model="email">
        </p>
        <p>
            <label for="password">Password</label> 
                <input type="password" id="password" v-model="password">
        </p>
        <p>
            <label for="passwordVerify">Verify Password</label> 
                <input type="password" id="passwordVerify" v-model="passwordVerify">
        </p>

        <p><input type="submit" value="Submit"></p>
      </form>

    </div>
    <div class="success-message" v-show="!showForm">
      <h1> Welcome {{ username }}! Thank you for signing up!</h1>
      <p>Please take our new member survey. <router-link to="Survey"> Click here</router-link>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      errors: [],
      username: '',
      email: '',
      password: '',
      passwordVerify: '',
      showForm: true,
      showError: false
    }
  },

  methods: {
    validateForm: function () {
      if((this.username != '') &&
        (this.email != '') &&
        (this.password != '') &&
        (this.password === this.passwordVerify)) {
        this.showForm = false;
      } 
        
      this.errors = [];
      if (this.username === '') {
        this.showError = true;
        this.showForm = true;
        this.errors.push("Username required.");
        console.log('username is NOT valid');
      }
      if (this.email === '') {
        this.showForm = true;       
        this.showError = true;
        this.errors.push("Email required.");
        console.log('email is NOT valid.');
      }
      if ((this.password === '') ||
         (this.passwordVerify === '')) {
        this.showForm = true;          
        this.showError = true;
        this.errors.push("Password required.");
        console.log('password is NOT valid.');        
      } 
      if (this.password != this.passwordVerify) {
        this.showForm = true;          
        this.showError = true;
        this.errors.push("Passwords do not match.");
        console.log('password is NOT valid.');        
      }
    }
  }
}
        
</script>

<!-- "scoped" attribute limits CSS to this component only -->
<style scoped>
.error {
  border: 1px solid #aa0000;
  padding: 1rem;
  color: #aa0000;
}
h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
