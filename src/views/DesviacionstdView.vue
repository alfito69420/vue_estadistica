<template>
  <div class="flex flex-col items-center">
    <h1 class="text-center mt-6">DESVIACION ESTANDAR</h1>
    <input
      class="text-center mt-4"
      type="text"
      placeholder="Introduce tus numeros"
      v-model="numerosString"
    />
    <button class="btn mt-4" @click="calculardesviacion">Calcular</button>
    <h1 class="text-center mt-4">La Desviacion Estandar es: {{ desviacion }}</h1>
    <h1 class="text-center mt-4" v-if="errorMessage">{{ errorMessage }}</h1>

    <h1 class="text-center mt-4">Body: {{ numerosString }}</h1>
    <hr class="mt-4" />
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
const desviacion = ref(0);
const numerosString = ref('');
const errorMessage = ref('');


const calculardesviacion = async () => {
  try {

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

    console.log('numerosString:', numerosString.value);

    // Convertir la cadena de entrada a un array de números
    //const numeros = numerosString.value.split(',').map((num) => parseFloat(num.trim()));
    console.log('numeros:', numeros);

    // Asegurarse de que todos los elementos son números válidos
    if (numeros.some(isNaN)) {
      throw new Error('Uno o más elementos no son números válidos');
    }

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

    const url = 'https://nqvo8awo2c.execute-api.us-east-1.amazonaws.com/desviacion-estandar';
    const response = await fetch(url, options);

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const responseData = await response.json();
    console.log('responseData:', responseData);

    // Comprobar si la respuesta contiene la desviación estándar
    if (responseData.desviacionEstandar !== undefined) {
      desviacion.value = responseData.desviacionEstandar;
    } else {
      throw new Error('Respuesta del servidor no contiene la desviación estándar');
    }
  } catch (error) {
    console.error('Error:', error);
    //alert(error.message); // Mostrar alerta con el mensaje de error
  }
};
</script>

<style scoped>
.btn {
  @apply p-5 bg-blue-500 rounded mr-2 text-white cursor-pointer;
}
</style>
