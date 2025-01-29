<template>
    <nav class="flex justify-between items-center p-5">
        <div class="flex space-x-5">
            <NuxtLink to="/">STOP</NuxtLink>
            <NuxtLink to="/syntaxe">1</NuxtLink>
            <NuxtLink to="/auclick">2</NuxtLink>
            <NuxtLink to="/controls">3</NuxtLink>
            <NuxtLink to="/scroll">4</NuxtLink>
            <NuxtLink to="/tiles">5</NuxtLink>     
            <NuxtLink to="/accordion">6</NuxtLink>     

        </div>
    </nav>
</template>

<style>
.router-link-exact-active {
    @apply text-tealight;
}
</style>