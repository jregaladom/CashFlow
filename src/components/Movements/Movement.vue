<template>
      <div class="movement">
        <div class="content">
            <h4>{{ title }}</h4>
            <p>{{ description }}</p>
        </div>
        <div class="action">
            <img src="@assets/trash-icon.svg" alt="borrar" @click="remove" />
            <p :class="{
                'red': isNegative,
                'green': !isNegative
            }">{{ amountCurrency }}</p>
        </div>
    </div>
</template>
<script setup>
import { toRefs, defineProps, defineEmits, computed } from "vue";

const props = defineProps({
    title: {
        type: String,
    },
    description: {
        type: String,
    },
    id:{
        type: String,
    },
    amount: {
        type: Number,
    },
});

const { id, title, description, amount } = toRefs(props);

const isNegative = computed(() => {
    return amount.value < 0;
});

const amountVisual = computed(() => {
   return amount.value !== null ?  amount.value : 0;
});



const currencyFormater = (amount) => {
   return new Intl.NumberFormat(("es-MX"), {
      style: "currency", currency: "MXN"
   }).format(amount);
}

const amountCurrency = computed(() => {
   return currencyFormater(amountVisual.value);
});

const remove = () => {
  emit('removeElement', id.value)
}


const emit = defineEmits(['removeElement']);

</script>
<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
    color: red;
}

.green {
    color: green;
}
</style>