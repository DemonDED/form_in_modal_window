<template>
  <div>
    <input placeholder="First Name *" v-model="valueOfInput.firstName" type="text">
    <p class="warning" v-show="warningCheck">Pleace fill in firs name</p>
  </div>
  <div>
    <input placeholder="Last Name *" v-model="valueOfInput.lastName" type="text">
    <p class="warning" v-show="warningCheck">Pleace fill in last name</p>
  </div>
  <div>
    <input placeholder="user@gmail.com *" v-model="valueOfInput.userEmail" type="text">
    <p class="warning" v-show="warningCheck">Pleace fill in email</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
      valueOfInput: {
        firstName: null,
        lastName: null,
        userEmail: null,
      }
      }
    },
    methods: {

    }
  }
</script>

<style scoped>

</style>