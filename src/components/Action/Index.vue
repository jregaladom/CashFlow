<template>
    <button @click="showModal = true">
        Agregar movimiento
    </button>
    <Teleport to="#app">
        <Modal v-show="showModal" @close="showModal = false" >
            <form @submit.prevent="submit">
                <div class="field">
                    <label for="date">Titulo</label>
                    <input type="text" v-model="title">
                </div>
                <div class="field">
                    <label for="amount">Monto</label>
                    <input type="number" id="amount"  v-model="amount">
                </div>
                <div class="field">
                    <label for="description">Descripción</label>
                    <textarea rows="4" id="description"  v-model="description" />
                </div>
                <div class="field">
                    <label for="type" class="radio-label">
                        <input type="radio" id="type" name="type" value="income" v-model="type">
                        <span>Ingreso</span>
                    </label>
                    <label for="type" class="radio-label">
                        <input type="radio" id="type" name="type" value="expense" v-model="type">
                        <span>Gasto</span>
                    </label>
                </div>
                <div class="action">
                    <button type="submit">Agregar movimiento</button>
                </div>
            </form>
        </Modal>
    </Teleport>
</template>
<script setup>

import { ref, defineEmits } from 'vue';
import Modal from '@/components/Action/Modal.vue'

const showModal = ref(false);
const title = ref('');
const amount = ref(0);
const description = ref('');
const type = ref('income');


const emit = defineEmits(['create']);

const submit = () => {
    showModal.value = false;
    emit('create', {
        id: Math.random().toString(16).slice(2),
        title: title.value,
        amount: type.value === 'income' ? amount.value : -amount.value,
        description: description.value,
        time: new Date('2023-06-06'),
       
    });
    title.value = '';
    amount.value = 0;
    description.value = '';
    type.value = 'income';
    
}


</script>
<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>