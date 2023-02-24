<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    aphorism: {
      type: String,
      required: true,
    },
    imageUrl: {
      type: String,
      required: true,
      default:
        'https://images.unsplash.com/photo-1432889490240-84df33d47091?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=3132&q=80',
    },
  },
});
</script>

<template>
  <div>
    <img :src="imageUrl" width="500" height="420" />
    <p class="aphorism">{{ aphorism }}</p>
  </div>
</template>

<style scoped>
div {
  position: relative;
}

img {
  width: 100%;
  max-width: 500px;
  border-radius: 10px;
  box-shadow: 0 0 10px #000;
  object-fit: cover;
}

.aphorism {
  position: absolute;
  max-width: 500px;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 2rem;
  font-style: italic;
  text-shadow: 0 0 2px #000;
}
</style>
