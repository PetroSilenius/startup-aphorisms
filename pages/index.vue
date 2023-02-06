<script setup lang="ts">
import Aphorism from '../components/Aphorism.vue';

const headers = {
  'Content-Type': 'application/json',
  Authorization: 'Bearer ' + process.env.OPENAI_API_KEY,
};

const prompt = 'Write a short inspirational goal-oriantated aphorism for a startup';

const { data: texts, error } = await useFetch<{
  choices: [
    {
      text: string;
      index: number;
      logprobs: null;
      finish_reason: string;
    }
  ];
}>('https://api.openai.com/v1/completions', {
  headers,
  method: 'POST',
  body: JSON.stringify({
    prompt,
    max_tokens: 5,
    temperature: 0.9,
    model: 'text-ada-001',
  }),
});

console.log({ texts, error });

const aphorism = texts?.value?.choices[0].text;
if (!aphorism) {
  throw new Error('No aphorism found');
}

const { data: images } = await useFetch<{ data: [{ url: string }] }>(
  'https://api.openai.com/v1/images/generations',
  {
    headers,
    method: 'POST',
    body: JSON.stringify({
      prompt:
        'A slightly blurred background image with a thoughtful environment that matches the aphorism' +
        aphorism,
      n: 1,
      size: '500x420',
    }),
  }
);

console.log({ images });

const imageUrl = images?.value?.data[0].url;
</script>

<template>
  <div class="grid">
    <div>
      <h1>"{{ prompt }}"</h1>
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
