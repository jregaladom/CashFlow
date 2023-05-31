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
                    <Action/>
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" />
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
import { computed } from 'vue';

const movements = [
{
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 10,
          time:new Date('2023-05-01')
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 134,
          time:new Date('2023-05-14')
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
          time:new Date('2023-05-14')
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 300,
          time:new Date('2023-05-17')
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: 500,
          time:new Date('2023-05-20')
        },
        {
          id: 6,
          title: "Movimiento 6",
          description: "Autobus",
          amount: -50,
          time:new Date('2023-03-19')
        },
];





const amounts = computed(() => {
  const _amount = movements.filter((m) =>{
  const currentDay = new Date();
  const oldDate =  new Date( (currentDay.getDate() - 30));
  return m.time >= oldDate && m.time <= currentDay;
}).map(m => m.amount);
  return _amount;
});






</script>
