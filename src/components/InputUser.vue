<script setup>
const model = defineModel()
import PersonIcon from './icons/PersonIcon.vue'
</script>

<template>
  <form>
  <PersonIcon />
 <input placeholder="name" v-model="model">
 
  </form>
</template>

<style scoped>
form {
display:flex;
align-items:center;
gap:10px;
float:right
}

input {
  border: none;
  border-bottom: 2px solid #818181;
  padding: 8px;
  font-size: 16px;

  outline: none;

}

input:focus {

}

input::placeholder {
  color: #818181;
}
</style>