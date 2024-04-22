<template>
    <div>
        <h2>Edit Post</h2>
        <form @submit.prevent="saveChanges">
            <label for="title">Title:</label>
            <input type="text" id="title" v-model="post.title" required>

            <label for="body">Body:</label>
            <textarea id="body" v-model="post.body" required></textarea>

            <button type="submit">Save Changes</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    post: { type: Object, required: true },
});

const saveChanges = () => {
    // Aquí puedes enviar los cambios al servidor para actualizar el post
    // Por ejemplo, puedes hacer una llamada a la API para guardar los cambios en la base de datos
    console.log('Changes saved:', post.value);
}
</script>