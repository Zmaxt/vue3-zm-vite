<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" /> -->
  
  <div>
      <vote title="vue3.0"></vote>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Vote from './components/Vote.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    Vote
  }
}
</script>
