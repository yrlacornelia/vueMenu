<script setup>
import { ref, onMounted } from 'vue';
import DeleteIcon from './icons/DeleteIcon.vue';

const menu = ref({
  Monday: '',
  Tuesday: '',
  Wednesday: '',
  Thursday: '',
  Friday: '',
  Saturday: '',
  Sunday: '',
});

const selectedField = ref('Monday');
const inputValue = ref('');


onMounted(() => {
  const storedMenu = localStorage.getItem('menu');
  if (storedMenu) {
    Object.assign(menu.value, JSON.parse(storedMenu));
  }
});

const updateField = () => {
  if (selectedField.value && inputValue.value) {
    menu.value[selectedField.value] = inputValue.value;
    inputValue.value = '';
    saveToLocalStorage();
  } else {
    alert('Please select a day and enter a value');
  }
};

const deleteField = (day) => {
  menu.value[day] = '';
  saveToLocalStorage();
};

const saveToLocalStorage = () => {
  localStorage.setItem('menu', JSON.stringify(menu.value));
};


</script>



<template>

<form @submit.prevent="updateField">
    <div class="formItem">
      <label for="day">Day:</label>
      <select id="day" v-model="selectedField">
        <option v-for="(value, key) in menu" :key="key" :value="key">
          {{ key }}
        </option>
      </select>
    </div>
    <div class="formItem">
      <label for="dish">Dish:</label>
      <input id="dish" type="text" v-model="inputValue" placeholder="Lasagna" />
    </div>
    <button type="submit">Add</button>
  </form>


    <ul>
      <li v-for="(value, key) in menu" :key="key">
        <p>{{ key }}</p>
        <div class="inputfieldContainer">
          <h3>{{ value }}</h3>

          <button v-if="value" @click="deleteField(key)">
            <DeleteIcon />
          </button>
        </div>
      </li>
    </ul>

</template>


<style scoped>

button{
  border:none;
  cursor:pointer;
}



.inputfieldContainer {
  display: flex;
  align-items: center;
  justify-content: space-around;
  margin-top:2rem;

}
/* List  */
ul {

  display: grid;
  grid-template-columns: repeat(3, 1fr); 
  gap: 30px; 
  list-style-type: none;
  padding: 0;

}
li {
  background-color: #f0f0f0;
  padding: 10px;
  text-align: center;
  height:10rem;
  position:relative;
}
li p {
  -webkit-box-shadow: 10px 7px 56px -4px rgba(156,156,156,0.71);
-moz-box-shadow: 10px 7px 56px -4px rgba(156,156,156,0.71);
box-shadow: 10px 7px 56px -4px rgba(156,156,156,0.71);
position:absolute;
margin-top:-20px;
background-color:pink;
padding:0.8rem;
 left: 50%; 
transform: translateX(-50%);
width:6rem;

}
 li:nth-child(odd) p {
  transform: translateX(-50%) rotate(-2deg); 
  background-color:#E3F6EA;
}

 li:nth-child(even) p {
  transform: translateX(-50%) rotate(2deg); 
    background-color:#B0E7C6;

}




/* form  */
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 20%; 
  margin:auto;
  margin-bottom:3rem;
}

form > * {
  width: 100%; 
  margin: 10px 0; 
  box-sizing: border-box; 
}
form button{
border: none; 
background-color:#F0754F;
  color: white; 
  padding: 12px 24px; 
  font-size: 16px; 
  border-radius: 5px; 
  transition: background-color 0.3s ease; 
}

form button:hover {
  background-color: #DF5328; 

}

label {
  margin-right: 10px;
  font-weight: bold;
  color: #555;
}

input[type="text"] {
  padding: 10px;
  border: 1px solid #818181;;
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 10px;
  font-size: 16px;
}



select {
  padding: 10px;
  border: 1px solid #818181;;
  border-radius: 4px;
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 10px;
  font-size: 16px;
  background: #fff;
}
</style>



