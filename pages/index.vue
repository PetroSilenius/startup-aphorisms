<script setup lang="ts">
import Aphorism from '../components/Aphorism.vue';

const aphorism = "Don't be afraid to fail";
const imageUrl = 'https://source.unsplash.com/random/500x420';
</script>

<template>
  <div>
    <div class="grid">
      <div>
        <h1>"Write an aphorism for a startup that fits with a nice background image"</h1>
        <Aphorism :aphorism="aphorism" :imageUrl="imageUrl" />
      </div>
      <div>
        <h2>What is startup-aphorisms?</h2>
        <p>
          Startup-aphorisms is a project that uses OpenAI's API to generate generic aphorisms about
          startup culture.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-size: 2.5rem;
  font-weight: 600;
  text-shadow: 0 0 2px #000;
  margin-bottom: 6rem;
}

.grid {
  display: grid;
  place-items: center;
  height: 100vh;
  padding: 0 15px;
  text-align: center;
  background: linear-gradient(
    45deg,
    hsla(333, 37%, 46%, 1) 10%,
    hsla(243, 10%, 47%, 1) 50%,
    hsla(197, 44%, 42%, 1) 100%
  );
}
</style>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
  color: #f8f4e3;
}
</style>
