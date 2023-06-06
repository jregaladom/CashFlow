<template>
    <Layout>
        <template #header>
            <Header/>
        </template>
        <template #resume>
            <Resume :label="'Ahorro Total'"  :total-amount="100000" >
                <template #graphic>
                    <Graphic :amounts="amounts" />
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
import { computed, ref } from 'vue';

const movements = ref([]);

// const movements = ref([
// {
//           id:Math.random().toString(16).slice(2),
//           title: "Movimiento",
//           description: "Deposito de salario",
//           amount: 10,
//           time:new Date('2023-05-01')
//         },
//         {
//           id: Math.random().toString(16).slice(2),
//           title: "Movimiento 1",
//           description: "Deposito de honorarios",
//           amount: 60,
//           time: new Date('2023-05-14')
//         },
//         {
//           id:Math.random().toString(16).slice(2),
//           title: "Movimiento 3",
//           description: "Comida",
//           amount: -100,
//           time: new Date('2023-05-14')
//         },
//         {
//           id:Math.random().toString(16).slice(2),
//           title: "Movimiento 4",
//           description: "Colegiatura",
//           amount: 300,
//           time: new Date('2023-05-17')
//         },
//         {
//           id:Math.random().toString(16).slice(2),
//           title: "Movimiento 5",
//           description: "Reparación equipo",
//           amount: 500,
//           time: new Date('2023-05-20')
//         },
//         {
//           id: Math.random().toString(16).slice(2),
//           title: "Movimiento 6",
//           description: "Autobus",
//           amount: -50,
//           time: new Date('2023-05-19')
//         },
// ]);

const create = (inMovement) => {
 movements.value.push(inMovement);
};

const remove = (id) => {
  const index = movements.value.findIndex((m) => m.id === id);
  movements.value.splice(index, 1);
};

const amounts = computed(() => {
  const _amount = movements.value.filter((m) =>{
  const currentDay = new Date();
  const oldDate =  new Date( (currentDay.getDate() - 30));
  return m.time >= oldDate;
}).map(m => m.amount);

return _amount.map((m, i) => {
        const lastMovements = _amount.slice(0, i);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement
        }, 0);
      });
});


const save = () => {
  localStorage.setItem('movements', JSON.stringify(movements.value));
}







</script>
