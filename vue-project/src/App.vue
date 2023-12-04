<script setup>
import { reactive } from 'vue';

const estado = reactive({
  contador: 0,
  email: '',
  saldo: '5.000',
  transferir: '',
  saldoAtual: '',
  nomes: ["paulo", "gian"],
  inserirNome: ''
})

function criarEmail(e) {
  estado.email = e.target.value
}



function incrementar() {
  estado.contador++
}

function decrementar() {
  estado.contador--
}

function transferencia() {
  const { saldo, transferir } = estado

  return saldo - transferir
}

function valorTrasferido(e) {
  estado.transferir = e.target.value
}

function novoNome(e) {
  estado.inserirNome = e.target.value
}

function inserir() {
  estado.nomes.push(estado.inserirNome)
}






</script>

<template>
  <header>
    <div>
      <h1>teste</h1>


      {{ estado.contador }}

      <button type="button" @click="incrementar()">+</button>
      <button type="button" @click="decrementar()">-</button>

      <hr>
      {{ estado.email }} <br>
      <input type="email" @keyup="criarEmail">

      <hr>
      saldo: {{ estado.saldo }} <br>
      transferir: {{ estado.transferir }} <br>
      saldo atual: {{ transferencia() }} <br>
      <input :class="{ invalid: estado.transferir > estado.saldo }" @keyup="valorTrasferido" type="number"
        placeholder="saldo para transferencia">

      <hr>

      <br>

      <input type="text" @keyup="novoNome">
      <button type="submit" @click="inserir">inserir</button>

      <ul>
        <li v-for=" nome in estado.nomes">
          {{ nome }}

        </li>
      </ul>
    </div>
  </header>
</template>

<style scoped>
.invalid {
  outline-color: red;
  border-color: red;
}
</style>
