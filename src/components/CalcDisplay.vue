<script setup lang="ts">
    interface CalcDisplayProps {
        result?: string | number
    }

    const props: CalcDisplayProps = withDefaults(defineProps<CalcDisplayProps>(), {
        result: 0,
    });
</script>

<template>
    <div class = 'display'>{{ props.result }}</div>
</template>

<style scoped>
.display {
    grid-column: 1/5;
    display: flex;
    font-size: 50px;
    align-items: center;
    justify-content: right;
    padding-right: 10px;
    background-color: #333;
    color: white;
    border-radius: 5px;
    margin: 10px;
  }
</style>