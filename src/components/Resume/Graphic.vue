import { computed } from 'vue';
<template>
    <div>
        <svg viewBox="0 0 300 200">
            <line 
             stroke="#c4c4c4"
             stroke-with="2"
             x1="0"
             y1="100"
             x2="300"
             y2="100"
            />
            <polyline 
                fill="none"
                stroke="#0689B0"
                stroke-width="2"
                :points="points"/>
                <line 
                stroke="#04b500"
                stroke-with="2"
                x1="200"
                y1="0"
                x2="200"
                y2="200"/>

        </svg>
        <p>Últimos 30 días</p>
        {{ points  }}
    </div>
</template>
<script setup>
import { computed, defineProps, toRefs } from 'vue';

const props = defineProps({
    amounts: {
        type: Array,
        default: () => [],
    },
});

const { amounts } = toRefs(props);


const points = computed(() => {
   const total = amounts.value.length;
   const x = 300 / (total - 1);
    return amounts.value.map((amount, index) => {
        const y = 100 - (amount * 100) / 1000;
        return `${index * x},${y}`;
    }).join(' ');
});
</script>
<style scoped>
svg{
    width: 100%;
}
p {
    text-align: center;
}
</style>