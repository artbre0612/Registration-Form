<script setup>
import RegistrationForm from './components/RegistrationForm.vue'
</script>

<template>
  <RegistrationForm />
</template>


<style>
/* global style setting */
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Noto Sans TC", sans-serif;
  font-weight: 400;
}

body {
  background: url('/bg-img.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  backdrop-filter: blur(5px);
}

#app {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

@media screen and (max-width: 600px) {
  #app {
    margin: 25px 0;
  }
}


</style>