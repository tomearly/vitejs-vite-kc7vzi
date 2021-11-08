<script>
import { useVuelidate } from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'
import { reactive } from 'vue'

export default {
  setup () {
    const state = reactive({
      firstName: '',
      lastName: '',
      contact: {
        email: ''
      }
    })
    const rules = {
      firstName: { required }, // Matches state.firstName
      lastName: { required }, // Matches state.lastName
      contact: {
        email: { required, email } // Matches state.contact.email
      }
    }

    const v$ = useVuelidate(rules, state)

    return { state, v$ }
  }
}
</script>

<template> 
  <div>
    <label>
      First name
    </label>
      <input v-model="state.firstName" @blur="v$.firstName.$touch">
      <div v-if="v$.firstName.$error">Firstname field has an error.</div>
    <label>
      Last name
    </label>
      <input v-model="state.lastName" @blur="v$.lastName.$touch">
      <div v-if="v$.lastName.$error">Lastname field has an error.</div>
    <label>
      Email
    </label>
      <input v-model="state.contact.email" @blur="v$.contact.email.$touch">
      <div v-if="v$.contact.email.$error">Email field has an error.</div>

      <hr>
<p
  v-for="error of v$.$errors"
  :key="error.$uid"
>
<strong>{{ error.$validator }}</strong>
<small> on property</small>
<strong>{{ error.$property }}</strong>
<small> says:</small>
<strong>{{ error.$message }}</strong>
</p>

<pre>{{ v$ }}</pre>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
