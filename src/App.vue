<script setup>
import Home from '@/components/Home.vue'
import Splashscreen from '@/components/Splashscreen.vue'
import { defineAsyncComponent } from 'vue';

const HomeC = defineAsyncComponent(() => {
  new Promise((resolve) => {
    setTimeout(() => {
      resolve(Home);
    }, 3000);
  });
});

</script>

<template>
    <Suspense>
        <template #default>
            <Home />
        </template>
        <template #fallback>
            <Splashscreen />
        </template>
    </Suspense>
</template>

<style scoped>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
* {
  --brand-green: #04b500;
  --brand-blue: #070707;
}
</style>
