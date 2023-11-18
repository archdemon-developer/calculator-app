<script setup lang = "ts">
        interface CalcTitleProps {
        title?: string
    }

    const props: CalcTitleProps = withDefaults(defineProps<CalcTitleProps>(), {
        title: 'VUE CALCULATOR',
    });
</script>
<template>
    <h1 class="title">{{ props.title }}</h1>
</template>