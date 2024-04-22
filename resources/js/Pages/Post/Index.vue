<script setup>
import { ref, onMounted } from 'vue';
import { Link, router } from '@inertiajs/vue3';

const posts = ref([]);

onMounted(() => {
    getPosts();
});

const getPosts = async () => {
    try {
        const response = await axios.get('/api/posts');
        posts.value = response.data;
    } catch (error) {
        console.error(error);
    }
}

const deletePost = async (slug) => {
    try {
        const response = await axios.delete(`/api/posts/${slug}`);
        window.location.reload();
    } catch (error) {
        console.error(error);
    }
}

const editPost = (slug) => {
    router.get(route('post.edit', slug));
}
</script>

<template>
    <div
        class="container w-full bg-white border shadow-sm rounded-xl dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70">
        <h1 class="text-4xl text-white text-center font-bold mx-auto">Posts</h1>
        <div v-for="post in posts" :key="post.id" class="container grid grid-cols-3 gap-4">
            <Link :href="route('post.detail', post.slug)">
            <div
                class="flex flex-col  mx-auto bg-white border shadow-sm rounded-xl dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70 w-1/2">
                <div class="p-4 md:p-7">
                    <h2 class="text-lg font-bold text-gray-800 dark:text-white">
                        {{ post.title }}
                    </h2>
                    <p v-html="post.body" class="mt-2 text-gray-500 dark:text-neutral-400">
                    </p>
                </div>
            </div>
            </Link>
            <div
                class="bg-white border shadow-sm rounded-xl dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70 flex items-center justify-center">
                <button class="bg-red-500 text-white px-4 py-2 rounded-md"
                    @click="deletePost(post.slug)">Delete</button>
            </div>
            <div
                class="bg-white border shadow-sm rounded-xl dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70 flex items-center justify-center">
                <button class="bg-blue-500 text-white px-4 py-2 rounded-md" @click="editPost(post.slug)">Edit</button>
            </div>
        </div>
    </div>
</template>
