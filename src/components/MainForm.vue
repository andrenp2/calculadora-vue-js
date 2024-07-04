<script setup>
import { reactive } from 'vue';
    const estado = reactive({
        operacao: '',
        num1: 0,
        num2: 0,
        resultado: 0
})

const somar = (a, b) => a + b;
const subtrair = (a, b) => a - b;
const dividir = (a, b) => (b != 0 ? a / b : 'Erro: Divisão por zero.');
const multiplicar = (a, b) => a * b;

const calcularResultado = () => {
  const { operacao, num1, num2 } = estado;

  switch (operacao) {
    case 'somar':
      estado.resultado = somar(num1, num2);
      break;
    case 'dividir':
      estado.resultado = dividir(num1, num2);
      break;
    case 'subtrair':
      estado.resultado = subtrair(num1, num2);
      break;
    case 'multiplicar':
      estado.resultado = multiplicar(num1, num2);
      break;
    default:
      estado.resultado = '...';
  }
};
</script>

<template>
    <form @submit.prevent="calcularResultado">
        <div class="row">
            <div class="col-3"></div>
            <div class="col-2">
                <input v-model="estado.num1" class="form-control" required type="number" placeholder="Digite o primeiro número.">
            </div>
            <div class="col-2">
                <input v-model="estado.num2" class="form-control" required type="number" placeholder="Digite o segundo número.">
            </div>
            <div class="col-2">
                <select v-model="estado.operacao" class="form-control">
                    <option value="somar">Somar</option>
                    <option value="subtrair">Subtrair</option>
                    <option value="multiplicar">Multiplicar</option>
                    <option value="dividir">Dividir</option>
                </select>
            </div>
            <div class="col-2">
                <button type="submit" class="btn btn-primary">Calcular</button>
            </div>
            <div class="col-3"></div>
        </div>
        <div class="row">
            <p class="mt-5 text-center fs-5">
                {{ estado.resultado }}
            </p>
        </div>
    </form>
</template>