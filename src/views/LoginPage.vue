<template>
  <form class="" @submit.prevent>
    <div>
      <label for="username">Username</label>
      <input id="username" v-model="username" type="text" placeholder="Username">
    </div>
    <div>
      <label for="password" class="">Password</label>
      <input id="password" v-model="password" type="password" placeholder="Password">
    </div>
    
    <button @click="logUserin" class="">LOGIN</button>
  </form>
</template>

<script setup>
import  {ref} from 'vue';
import { useRoute, useRouter } from 'vue-router';
import {useAuth} from '../composables/useAuth.js'

const {login, logout} = useAuth();

const router = useRouter();
const route = useRoute();

const username = ref('');
const password = ref('');

const logUserin = async () => {
  if (await login(username.value, password.value)) {
    if (route.query.redirect) {
      router.push(route.query.redirect);
    } else {
      router.push({name: 'SettingsPage'})
    }
  } else {
    logout()
  }
}
</script>