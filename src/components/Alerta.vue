<script setup>
import { computed } from 'vue';

    const props = defineProps({
        alerta: {
            type: Object,
            required: true,
        }
    });

    //const isError = computed(() => props.alerta.color === 'red');
</script>
<template>
    <!-- :class = "isError ? 'bg-red-500' : 'bg-green-500'" -->
    <div
        :class= "'bg-'+ alerta.color +'-500'"
        class ="text-white text-center p-3 uppercase font-bold mb-3 rounded-md"
    >
        {{ alerta.mensaje }}
    </div>
</template>
