<script setup>
    import { reactive  } from 'vue';

    const calculo = reactive ({
    firstNumber: '',
    secondNumber: '',
    operation: 'adicionar',
    operations: {
        dividir: (n1, n2) => (n2 === 0 ? 'Não divida por zero' : n1 / n2),
        multiplicar: (n1, n2) => n1 * n2,
        adicionar: (n1, n2) => n1 + n2,
        subtrair: (n1, n2) => n1 - n2
    },
    resultado: 0,
    });

    const calculadora = () => {
    const num1 = parseFloat(calculo.firstNumber);
    const num2 = parseFloat(calculo.secondNumber);
    calculo.resultado = !isNaN(num1) && !isNaN(num2) ? calculo.operations[calculo.operation](num1, num2) : 0;
    }
</script>

<template>
    <div class="container mt-5">
        <div class="row justify-content-center">
        <form class="col-md-6 form-group">
            <div>
            <label for="numero1">Número 1</label>
            <input type="number" class="form-control" id="numero1" v-model="calculo.firstNumber" @input="calculadora"/>
            </div>
            <div>
            <label for="numero2">Número 2</label>
            <input type="number" class="form-control" id="numero2" v-model="calculo.secondNumber" @input="calculadora" />
            </div>
            <div>
            <label for="operacao" >Operação</label>
            <select class="form-control" id="operacao" v-model="calculo.operation" @change="calculadora">
                <option value="adicionar">+</option>
                <option value="subtrair">-</option>
                <option value="multiplicar">*</option>
                <option value="dividir">/</option>
            </select>
            </div>
            <div class="mt-3">
            <label>{{ calculo.resultado }}</label>
            <output id="resultado" class="form-control"></output>
            </div>
        </form>
        </div>
    </div>
</template>