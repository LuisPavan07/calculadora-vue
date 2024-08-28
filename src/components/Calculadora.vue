<script setup>
import { reactive } from 'vue';

const estado = reactive({
    numeroCampo1: '',
    numeroCampo2: '',
    operacoes: {
        somar: (a, b) => a + b,
        subtrair: (a, b) => a - b,
        multiplicar: (a, b) => a * b,
        dividir: (a, b) => (b !== 0 ? a / b : 'Dividir por zero'),
    },
    operacao: 'somar',
    resultado: 0,
});

const calculaResultado = () => {
    const operacao = estado.operacoes[estado.operacao];
    estado.resultado = operacao(Number(estado.numeroCampo1), Number(estado.numeroCampo2));
};
</script>

<template>
    <div class="container">
        <h1 class="titulo">Calculadora Aritimética</h1>
        <input type="text" v-model="estado.numeroCampo1" @input="calculaResultado" />
        <input type="text" v-model="estado.numeroCampo2" @input="calculaResultado" />
        <select v-model="estado.operacao" @change="calculaResultado">
            <option value="somar"> Adição </option>
            <option value="subtrair"> Subtração </option>
            <option value="multiplicar"> Multiplicação </option>
            <option value="dividir"> Divisão </option>
        </select>
        <span class="resultado">Resultado: {{ estado.resultado }}</span>
    </div>
</template>

<style scoped>
.container {
    max-width: 600px;
    margin: auto;
    margin-top: 40px;
    padding: 20px;
    text-align: center;
    background-color: rgb(92, 145, 243);
    border-radius: 24px;
}

input, select {
    display: block;
    width: 100%;
    text-align: end;
    margin-bottom: 16px;
    padding: 16px;
    font-size: 24px;
    border-radius: 24px;
}

.titulo {
    font-size: 40px;
    margin-bottom: 20px;
}

.resultado {
    font-size: 30px;
    font-weight: bold;
    border-bottom: 1px solid black;
}
</style>
