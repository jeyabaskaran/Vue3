<template>
  <section class="container">

    <div v-if="bitVal">
      <user-data v-if="bitVal" :firstName="firstName" :LAST="lastName" @emit-something="emitSomething"></user-data>
    </div>

    <h2>{{ user.userName }}</h2>
    <h3>{{ fullName }}</h3>
    <h2>{{ user.userAge }}</h2>
    <h3>{{ userName }}</h3>
    <button @click="setNewValue">Change value</button>


    <!-- <input type="text" @input="SetFirstName" />
    <input type="text" @input="SetLastName" /> -->

    <input type="text" v-model="firstName" /> <!--- Two way binding composition API -->
    <input type="text" ref="lastNameInput" />

    <button @click="setLastName">Set Last Name</button>
    <button @click="showComponent">Show/Disable</button>

  </section>
</template>

<script setup>

import { ref, reactive, isReactive, isRef, computed, watch, provide 
  , onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted} from 'vue';
import UserData from './Components/UserData.vue';

/** Composition API */

const userName = ref('Maximilian'); // -- ref is suitable for all kind of types
const firstName = ref('');
const bitVal= ref(false);
const lastName = ref('');
const lastNameInput = ref(null);
const user = reactive({  // -- reactive is suitable for only dealing with objects
  userName: 'Maxmilian',
  userAge: 32
});

// defineEmits([emitSomething]);


function showComponent(){
  bitVal.value=!bitVal.value;
}

console.log(isRef(userName));
console.log(isReactive(user));

onBeforeMount(()=>{
  console.log('Before mount');
});
onMounted(()=>{
  console.log('Mounted');
});

onBeforeUpdate(()=>{
  console.log('Before Update');
});
onUpdated(()=>{
  console.log('Update');
});

onBeforeUnmount(()=>{
  console.log('Before Unmounted');
});

onUnmounted(()=>{
  console.log('After Unmount');
});

function emitSomething() {
  alert('emit works');
}

function setNewValue() {
  user.userAge = 33;
  user.userName = 'data';
  userName.value = 'dummy';
}

provide('userage', user);
function setLastName() { //-- this.$refs not work in the composition API, instead we using like below.
  lastName.value = lastNameInput.value.value;
}
// function SetFirstName(event) {
//   firstName.value = event.target.value;
// }
// function SetLastName(event) {
//   lastName.value = event.target.value;
// }

const fullName = computed(function () {  // -- Computed properties 
  return firstName.value + " " + lastName.value;
});

watch([firstName, userName], function (newValue, oldValue) { // Watcher with composition APi, we can able to watch multiple fields at one time

  console.log(oldValue[0], newValue[0]);
  console.log(oldValue[1], newValue[1]);
});

// setTimeout(() => {
//   user.userName="data";
//   user.userAge=33;
// }, 2000);

/** Option API */
// data() {
//   return {
//     userName: 'Maximilian',
//   };
// },

</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>