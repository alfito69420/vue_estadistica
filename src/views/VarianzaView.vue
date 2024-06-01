<template>
  <div class="flex flex-col items-center">
    <h1 class="text-center mt-6">VARIANZA</h1>
    <input
      class="text-center mt-4"
      type="text"
      placeholder="Introduce tus numeros"
      v-model="numerosString"
    />
    <button class="btn mt-4" @click="calcularVarianza">Calcular</button>
    <h1 class="text-center mt-4">La varianza es: {{ varianza }}</h1>
    <h1 class="text-center mt-4" v-if="errorMessage">{{ errorMessage }}</h1>
    <h1 class="text-center mt-4">Body: {{ numerosString }}</h1>
    <hr />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
const varianza = ref(0);
const numerosString = ref('');
const errorMessage = ref('');

const calcularVarianza = async () => {
  errorMessage.value = '';

  if (!numerosString.value) {
    errorMessage.value = 'Por favor, introduce tus números.';
    return;
  }

  const numeros = numerosString.value.split(',').map(num => parseFloat(num.trim()));

  if (numeros.length < 20) {
    errorMessage.value = 'El array de números debe contener al menos 20 elementos.';
    return;
  }

  const url = 'https://nqvo8awo2c.execute-api.us-east-1.amazonaws.com/varianza';

  const data = {
    numeros: numeros,
  };

  const options = {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(data),
  };

  try {
    const response = await fetch(url, options);
    const responseData = await response.json();
    varianza.value = responseData.varianza;
    console.log('varianza:', varianza.value);
  } catch (error) {
    console.error('Error:', error);
  }
};
</script>

<style scoped>
.btn {
  @apply p-5 bg-blue-500 rounded mr-2 text-white cursor-pointer;
}
</style>
