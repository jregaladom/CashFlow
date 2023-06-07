<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume :label="'Ahorro Total'" :total-amount="totalAmount" :amount="amount" >
                <template #graphic>
                    <Graphic :amounts="amounts" @select="select" :date-amount="dateAmount" />
                </template>
                <template #action >
                    <Action @create="create"/>
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" @remove="remove" />
        </template>
    </Layout>
</template>
<script setup>
import Layout from '@/components/Layout.vue';
import Header from '@/components/Header.vue';
import Resume from '@/components/Resume/Index.vue';
import Movements from '@/components/Movements/Index.vue';
import Action from '@/components/Action/Index.vue';
import Graphic from '@/components/Resume/Graphic.vue';
import { computed, ref, onMounted } from 'vue';

const movements = ref([]);
const amount = ref(null);
const dateAmount = ref('Últimos 30 días');

const create = (inMovement) => {
 movements.value.push(inMovement);
 save();
};

const remove = (id) => {
  const index = movements.value.findIndex((m) => m.id === id);
  movements.value.splice(index, 1);
  save();
};

onMounted(() => {
  const movementsFromLocalStorage = localStorage.getItem("movements");
  if (movementsFromLocalStorage) {
    movements.value = JSON.parse(movementsFromLocalStorage)?.map(
      (movement) => ({
        ...movement,
        time: new Date(movement.time),
      })
    );
  }
})

const totalAmount = computed(() => {
    const total = movements.value.reduce((acc, movement) => {
        return acc + movement.amount;
    }, 0);

    return total;
});

const amounts = computed(() => {
    const _amount = movements.value.filter((m) =>{
      const today = new Date();
            const oldDate = today.setDate(today.getDate() - 30);

            return m.time > oldDate;
  }).map(m => m.amount);

  return _amount.map((m, i) => {
          const lastMovements = _amount.slice(0, i+1);

          return lastMovements.reduce((suma, movement) => {
            return suma + movement
          }, 0);
        });

});

const save = () => {
  localStorage.setItem("movements", JSON.stringify(movements.value));
}

const select = (value) => {
  console.log(value);
  amount.value = value.amount != null ? value.amount : null;
  dateAmount.value = value.index != null ? `Al día ${movements.value[value.index].time}`:  'Últimos 30 días' ; 
}
</script>
