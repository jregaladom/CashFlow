<template>
   <main>
      <p>{{ label }}</p>
      <h1>{{ amountCurrency }}</h1>
      <div class="graphic">
         <slot name="graphic"></slot>
      </div>
      <div class="action">
         <slot name="action"></slot>
      </div>

   </main>
</template>

<script setup>

import { toRefs, computed } from 'vue';

const props = defineProps(
    {
      label: String,
      amount: {
         type: Number,
         default: null,
      },
      totalAmount: Number,
  }
  );

const {label, amount, totalAmount} = toRefs(props);

const amountVisual = computed(() => {
   return amount.value !== null ? amount.value : totalAmount.value;
});


const currencyFormater = (amount) => {
   return new Intl.NumberFormat(("es-MX"), {
      style: "currency", currency: "MXN"
   }).format(amount);
}

const amountCurrency = computed(() => {
   return currencyFormater(amountVisual.value);
});



</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>