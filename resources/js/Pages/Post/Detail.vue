<script setup>
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue';

const props = defineProps({
    post: { type: Object, required: true },
});
</script>

<template>
    <h1>
        {{ post }}
    </h1>
</template>