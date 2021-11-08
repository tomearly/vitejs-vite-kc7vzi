<script setup>
import { useVuelidate } from '@vuelidate/core'
import CompA from '@/components/CompA'
import CompB from '@/components/CompB'

export default {
  components: { CompA, CompB },
  setup () {
    // this will collect all nested component’s validation results
    const v = useVuelidate()

    return { v }
  }
}
</script>

<template>
  <div>
    <label>
      <input v-model="name">
      <div v-if="v$.name.$error">Name field has an error.</div>
    </label>
    <!-- this will contain all $errors and $silentErrors from both <CompA> and <CompB>-->
    <p v-for="error of v.$errors" :key="error.$uid">
      {{ error.$message }}
    </p>
  </div>
</template>

<script>

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
