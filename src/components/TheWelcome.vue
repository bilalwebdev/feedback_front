<script setup>
import WelcomeItem from './WelcomeItem.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
import ToolingIcon from './icons/IconTooling.vue'
import EcosystemIcon from './icons/IconEcosystem.vue'
import CommunityIcon from './icons/IconCommunity.vue'
import SupportIcon from './icons/IconSupport.vue'

import { ref } from 'vue';
import axios from 'axios'

const form = ref({
  email: '',
  password: ''
})

axios.defaults.withCredentials=true;

const user = ref();

async function onLogin(){
  await axios.get('http://localhost:8000/sanctum/csrf-cookie');
  await axios.post('http://localhost:8000/login', {
    email: form.value.email,
    password: form.value.password,
  })
}


let {data} = axios.get('http://localhost:8000/api/user');

user.value = data;



</script>

<template>
   <form @submit.prevent="onLogin" action="">

    <div class="">
      {{ user }}
      <label for="">Email</label>
      <input v-model="form.email" type="text" name="email" />
    </div>
    <div class="">
      <label for="">Password</label>
      <input v-model="form.password" type="password" name="password" />
    </div>

   <button type="submit">Submit</button>

   </form>
</template>
