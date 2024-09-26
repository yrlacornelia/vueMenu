<script setup>

import ListMenu from './components/ListMenu.vue'
import { ref } from 'vue'
const name = ref('') 

import Child from './components/InputUser.vue'
</script>

<template>

  <main>
  

  <Child v-model="name" />

      <h2 v-if="name"> {{ name }}´s Meal planner</h2>
       <h2 v-else>Meal Planner</h2>
       
      <ListMenu />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}
main{
  margin:auto;
  background-color:white;
  border-radius:1rem;
  padding: 4rem;
}

h2{
  margin-top:4rem ;
    margin-bottom:1.5rem ;
  font-size:40px;
  color:#48C77B;
text-transform: uppercase;
text-align: center;
  font-family: 'Fredoka One';

}


@media (min-width: 1024px) {

}
</style>
