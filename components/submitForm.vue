<template>
  <div class="submitPage">
    <div class="form">
      <form
        @submit="check"
      >
        <p v-if="errors.length">
          <b>Please correct the following error(s):</b>
          <ul>
            <li v-for="error in errors" :key="error.id">
              {{ error }}
            </li>
          </ul>
        </p>
        <label for="name">name</label>
        <input
          id="name"
          v-model="users.name"
          type="text"
          placeholder="What's your name?"
        >
        <label for="lastname">Lastname</label>
        <input
          id="lastname"
          v-model="users.lastname"
          type="text"
          placeholder="What's your last name?"
        >
        <br>
        <label for="age">Age</label>
        <input
          id="age"
          v-model="users.age"
          type="number"
          placeholder="How old are you?"
        >
        <br>
        <label for="email">Email</label>
        <input
          id="email"
          v-model="users.email"
          type="text"
          placeholder="What's your email?"
        >
        <br>
        <label for="password">Password</label>
        <input
          id="password"
          v-model="users.password"
          type="password"
          placeholder="Password"
        >
        <label for="confirmPassword">Confirm password</label>
        <input
          id="confirmPassword"
          v-model="confirmPassword"
          type="password"
          placeholder="Confirm your password"
        >
        <p>
          <input
            type="submit"
            value="Submit"
          >
        </p>
        {{ users.name }}
        {{ users.lastname }}
        {{ users.email }}
        {{ users.password }}
        {{ users.confirmPassword }}
      </form>
    </div>
    <h1 style="text-align: center;">
      Users Data
    </h1>
    <!-- <div v-for="user in users" :key="user.id" class="userList">
      {{ user }}
    </div> -->
  </div>
</template>

<script>
export default {
  data () {
    return {
      errors: [],
      users: [{
        name: '',
        lastname: '',
        age: '',
        email: '',
        password: ''
      }],
      confirmPassword: ''
    }
  },
  methods: {
    check: function (e) {
      this.errors = []

      if (!this.users.name) {
        this.errors.push('Name required.')
      }
      if (!this.users.lastname) {
        this.errors.push('Last Name required.')
      }
      if (!this.users.age) {
        this.errors.push('Age required.')
      }
      if ((this.users.age <= 0) || (this.age >= 123)) {
        this.errors.push('proper age required.')
      }
      if (!this.users.email) {
        this.errors.push('Email required.')
      } else if (!this.validEmail(this.users.email)) {
        this.errors.push('Valid email required.')
      }
      if (!this.users.password) {
        this.errors.push('Password required.')
      }
      if ((this.users.password) && (this.users.password.length < 8)) {
        this.errors.push('Password must be between 8 - 20 character.')
      }
      if (this.confirmPassword !== this.users.password) {
        this.errors.push('Password not match.')
      }
      if (!this.errors.length) {
        // eslint-disable-next-line no-console
        console.log(this.users)
        return true
      }

      e.preventDefault()
    },
    validEmail: function (email) {
      const valid = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      return valid.test(email)
    }
  }
}
</script>

<style>
.submitPage{
    display: flex;
    justify-content: center;
    width: 100%;
    height: 100%;
    flex-direction: column;
}
.form{
    background-color: orange;
    border: 1px solid black;
    padding: 3rem;
    margin: auto;
    width: auto;
    height: auto;
}
.userList{
    margin: auto;
}
</style>
