<script setup lang="ts">
    import { ref } from 'vue';
    import type { Ref } from 'vue';

    interface CalcButtonProps {
        text: string
        isCompute?: boolean,
        size?: number
    }

    const props: CalcButtonProps = withDefaults(defineProps<CalcButtonProps>(), {
        isCompute: false,
        size: 1
    });

    const calcbuttonClasses: Ref<string> = ref(`calc-button ${props.isCompute ? 'compute-button' : ''} size-${props.size}`);
</script>

<template>
    <button :class="calcbuttonClasses">{{ props.text }}</button>
</template>

<style scoped>
.calc-button {
    background-color: transparent;
    border: none;
    margin: 5px;
    font-size: 40px;
    cursor: pointer;
    background-color: #333;
    color: white;
    border-radius: 5px;
  }

  .calc-button:hover {
    background-color: #444;
  }

  .compute-button {
    background-color: #41B883;
  }

  .compute-button:hover {
    background-color: #70d7a9;
  }

  .size-2 {
    grid-column: 1/3;
  }

</style>