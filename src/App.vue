<script setup>
import { reactive, watch } from 'vue';

const estado = reactive({
    calculo1: '',
    calculo2: '',
    operacao: 'soma',
    resultado: 0
});

const calcular = () => {
    const numero1 = parseFloat(estado.calculo1);
    const numero2 = parseFloat(estado.calculo2);

    if (!isNaN(numero1) && !isNaN(numero2)) {
        switch (estado.operacao) {
            case 'soma':
                estado.resultado = numero1 + numero2;
                break;
            case 'subtracao':
                estado.resultado = numero1 - numero2;
                break;
            case 'multiplicacao':
                estado.resultado = numero1 * numero2;
                break;
            case 'divisao':
                estado.resultado = numero1 / numero2;
                break;
        }
    } else {
        estado.resultado = 0;
    }
};

watch(
    () => [estado.calculo1, estado.calculo2, estado.operacao],
    () => calcular(),
    { immediate: true }
);
</script>

<template>
    <div class="container">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Calculadora aritmética</h1>
        </header>
        <form>
            <div class="row">
                <div class="col">
                    <input @input="calculate" v-model="estado.calculo1" type="number" placeholder="Número 1"
                        class="form-control">
                </div>
                <div class="col-md-1">
                    <select @input="calculate" v-model="estado.operacao" class="form-control select">
                        <option value="soma">+</option>
                        <option value="subtracao">-</option>
                        <option value="multiplicacao">x</option>
                        <option value="divisao">/</option>
                    </select>
                </div>
                <div class="col">
                    <input @input="calculate" v-model="estado.calculo2" type="number" placeholder="Número 2"
                        class="form-control">
                </div>
            </div>
        </form>
        <p class="p-2 mt-2 bg-light rounded-3">
            O resultado é {{ estado.resultado }}
        </p>
    </div>
</template>
<style scoped>
.select {
    color: #fff;
    background-color: rgb(0, 119, 255);
    font-size: large;
    text-align: center;
}
</style>