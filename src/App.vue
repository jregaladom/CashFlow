<script setup>
import Splashscreen from '@/components/Splashscreen.vue'
import Home from '@/components/Home.vue'
import { defineAsyncComponent } from 'vue';

const HomeAsync = defineAsyncComponent(() => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(Home);
    }, 2500);
  });
});
</script>

<template>
  <Suspense>
    <template #default>
      <HomeAsync/>
    </template>
    <template #fallback>
      <Splashscreen/>
    </template>
  </Suspense>
</template>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
