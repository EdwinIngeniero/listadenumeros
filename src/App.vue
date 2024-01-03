<template>
  <div class="mensaje">
    <h1>{{ mensaje }}</h1>
  </div>
  
  <div class="contador">
    <h1 :class="Colores">{{ contador }}</h1>
  </div>
  
  <div class="incremento button-container">
    <button @click="Incremento()" class="btn btn-success">Incremento</button>
  </div>
  
  <div class="decremento button-container">
    <button @click="Decremento()" class="btn btn-danger">Decremento</button>
  </div>
  
  <div class="resetear button-container">
    <button @click="Resetear()" class="btn btn-secondary">Resetear</button>
  </div>
  
  <div class="ingresar button-container">
    <button @click="Ingresar()" :disabled="Bloquearnumero" class="btn btn-primary">Ingresar</button>
  </div>
  
  <div class="lista">
    <ul class="list-group mt-2">
      <h4>{{ "Numeros ingresados" }}</h4>
      <li v-for="(numeros, index) in lista" :key="index" class="list-group-item">
        <h4 style="color: royalblue;">{{ numeros }}</h4>
      </li>
    </ul>
  </div>
  
  <div class="lista2">
    <ul class="list-group mt-2">
      <h4>{{ "Numeros ordenados" }}</h4>
      <li v-for="(numeros, index) in Listaordenada" :key="index" class="list-group-item">
        <h4 style="color: royalblue;">{{ numeros }}</h4>
      </li>
    </ul>
  </div>
  
  <div class="suma mt-4 d-flex align-items-center">
    <label for="resultado" class="form-label me-2 mb-0" style="font-weight: bold;">Suma:</label>
    <input type="text" class="form-control" :value="Suma()" readonly style="width: 70px; height: 30px; color: black; text-align: center;">
  </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  const contador = ref(0);
  
  const lista = ref([]);
  
  const mensaje = "Ingreso de numeros";
  
  const Incremento = () => {
    contador.value++;
  }
  
  const Decremento = () => {
    contador.value = contador.value - 1;
  }
  
  const Resetear = () => {
    contador.value = 0;
  }
  
  const Ingresar = () => {
    lista.value.push(contador.value);
  }
  
  const Colores = computed(()=>{
    if(contador.value === 0){
      return "zero";
    }
  
    if(contador.value > 0){
      return "positive";
    }
  
    if(contador.value < 0){
      return "negative";
    }
  });
  
  const Bloquearnumero = computed(()=>{
    const numero = lista.value.find((num) => num === contador.value);
    return numero || numero === 0;
  });
  
  const Listaordenada = computed(()=>{
    const numero = [...lista.value];
    return numero.sort((a, b) => a - b);
  });
  
  const Suma = () =>{
    let sum = 0;
    for(const num of lista.value){
      sum += num;
    }
    return sum;
  }
  </script>
  
  <style scoped>
  /* Estilos generales del proyecto*/
  .mensaje {
    color: royalblue;
    position: absolute;
    top: 20PX;
    left: 440px;
  }
  
  .contador {
    position: absolute;
    top: 70px;
    left: 595px;
  }
  
  .incremento {
    position: absolute;
    top: 125px;
    left: 380px;
  }
  
  .decremento {
    position: absolute;
    top: 125px;
    left: 504px;
  }
  
  .resetear {
    position: absolute;
    top: 125px;
    left: 628px;
  }
  
  .ingresar {
    position: absolute;
    top: 125px;
    left: 752px;
  }
  
  .zero {
    color: black;
  }
  
  .positive {
    color: green;
  }
  
  .negative {
    color: red;
  }
  
  .lista {
    position: absolute;
    text-align: center;
    top: 175px;
    left: 380px;
  }
  
  .lista2 {
    position: absolute;
    text-align: center;
    top: 175px;
    left: 645px;
  }
  
  .suma {
    position: absolute;
    top: 0px;
    right: 2vw;
  }
  
  /* Algunos ajustes adicionales en los botones */
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }
  
  .button-container {
    display: flex;
    gap: 10px;
    margin-top: 10px;
    width: 120px; 
  }
  
  .button-container button {
    flex: 1; 
  }
  
  /* Algunos ajustes adicionales de las listas */
  .lista,
  .lista2 {
    max-width: 400px; 
    margin: 10px auto; 
  }
  
  /* Configuraciones generales en cambios de pantalla */ 
  @media (max-width: 700px) {
    .mensaje,
    .contador,
    .button-container button,
    .incremento,
    .decremento,
    .resetear,
    .ingresar,
    .lista,
    .lista2,
    .suma {
      position: static;
      width: auto;
      margin: 2px 0; 
      text-align: center;
    }
  }
  
  @media (max-width: 980px) {
    .mensaje,
    .contador,
    .button-container button,
    .incremento,
    .decremento,
    .resetear,
    .ingresar,
    .lista,
    .lista2,
    .suma {
      position: static;
      width: auto;
      margin: 2px 0; 
      text-align: center;
    }
  }
  
  /* Propiedades de los botones en pantallas mas paqueñas */
  @media (max-width: 700px) {
    .button-container {
      flex-direction: column;
      width: 50%; 
      margin: 0 auto;
      max-width: none; 
    }
  }
  
  @media (max-width: 980px) {
    .button-container {
      flex-direction: column;
      width: 50%; 
      margin: 0 auto;
      max-width: none; 
    }
  }
  
  /* Ubicacion de las listas en pantallas mas pequeñas */
  @media (max-width: 700px) {
    .lista,
    .lista2 {
      width: 50%; 
      margin: 0 auto;
      max-width: none; 
    }
  }
  
  @media (max-width: 980px) {
    .lista,
    .lista2 {
      width: 50%; 
      margin: 0 auto;
      max-width: none; 
    }
  }
  </style>