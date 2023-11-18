<script setup lang="ts">
  import { ref } from 'vue';
  import type { Ref } from 'vue';
  import CalcTitle from './components/CalcTitle.vue';
  import CalcButton from './components/CalcButton.vue'
  import CalcDisplay from './components/CalcDisplay.vue';

  let res: Ref<number> = ref(0);  
  let operation: Ref<string> = ref('');
  let first: Ref<number> = ref(0);
  let noOfDecimalPlaces: Ref<number> = ref(0);
  let isDecimal: Ref<boolean> = ref(false);
  let operations: string = '+-/%×';

  const clear = () : void => {
    res.value = 0;
    isDecimal.value = false;
    noOfDecimalPlaces.value = 0;
  };

  const updateExpression = (val : string) : void => {
   if(val === '-/+') {
    operation.value = "-/+";
    compute();
   } else if(val === '.') {
     isDecimal.value = true;
     noOfDecimalPlaces.value++;
   } else if(operations.includes(val)) {
    operation.value = val;
    first.value = res.value;
    isDecimal.value = false;
    noOfDecimalPlaces.value = 0;
    res.value = 0;
   } else {
    if(!isDecimal.value) {
      res.value = res.value * 10 + parseInt(val);
    } else {
      res.value = res.value + parseInt(val) * 10 ** (-1 * noOfDecimalPlaces.value);
      noOfDecimalPlaces.value++;
    }
   }
  }

  const compute = () => {
    if(operation.value === '+') {
      res.value = res.value + first.value;
    } else if(operation.value === '-') {
      res.value = first.value - res.value;
    } else if(operation.value === '/') {
      res.value = first.value / res.value;
    } else if(operation.value === '×') {
      res.value = first.value * res.value;
    } else if(operation.value === '-/+') {
      res.value = -1 * res.value;
    } else if(operation.value === '%') {
      res.value = first.value % res.value;
    }
  }
</script>

<template>
<div class = 'container'> 
  <CalcTitle />
  <div class = "calculator">
    <CalcDisplay :result ="res" />
    <CalcButton text="C" @click="clear"/>
    <CalcButton text="%" @click="updateExpression('%')"/>
    <CalcButton text="-/+" @click="updateExpression('-/+')"/>
    <CalcButton text="÷" isCompute @click="updateExpression('/')"/>
    <CalcButton text="1" @click="updateExpression('1')"/>
    <CalcButton text="2" @click="updateExpression('2')"/>
    <CalcButton text="3" @click="updateExpression('3')"/>
    <CalcButton text="+" isCompute @click="updateExpression('+')"/>
    <CalcButton text="4" @click="updateExpression('4')"/>
    <CalcButton text="5" @click="updateExpression('5')"/>
    <CalcButton text="6" @click="updateExpression('6')"/>
    <CalcButton text="-" isCompute @click="updateExpression('-')"/>
    <CalcButton text="7" @click="updateExpression('7')"/>
    <CalcButton text="8" @click="updateExpression('8')"/>
    <CalcButton text="9" @click="updateExpression('9')"/>
    <CalcButton text="×" isCompute @click="updateExpression('×')"/>
    <CalcButton text="0" :size="2" @click="updateExpression('0')"/>
    <CalcButton text="." @click="updateExpression('.')"/>
    <CalcButton text="=" isCompute @click="compute()"/>
  </div>
</div>
</template>

<style scoped>
  .container {
    max-width: 600px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .calculator {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    background: #555;
    width: 100%;
    border-radius: 5px;
  }
</style>
