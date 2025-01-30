<template>
    <div>
        <h1 class="text-3xl font-bold uppercase">{{ title }}</h1>
        <hr class="w-20 my-10 h-3 bg-beige">
        <h2 class="text-lg font-light">{{ subTitle }}</h2>
    </div>
</template>

<script setup>
 const props = defineProps({
   title: { type: String, required: true },
   subTitle: {type: String, required: true },
 });
</script>