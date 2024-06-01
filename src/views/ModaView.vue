<template>
  <div class="flex flex-col items-center">
    <h1 class="text-center mt-6">MODA</h1>
    <input
      class="text-center mt-4"
      type="text"
      placeholder="Introduce tus numeros"
      v-model="numerosString"
    />
    <button class="btn mt-4" @click="calcularModa">Calcular</button>
    <h1 class="text-center mt-4">La moda es: {{ moda }}</h1>
    <h1 class="text-center mt-4">Body: {{ numerosString }}</h1>
    <hr />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
const moda = ref(0);
const numerosString = ref('');

const calcularModa = async () => {
  const url = 'https://nqvo8awo2c.execute-api.us-east-1.amazonaws.com/moda';

  const numeros = JSON.parse(`[${numerosString.value}]`);

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
    moda.value = responseData.moda;
    console.log('moda:', moda.value);
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
