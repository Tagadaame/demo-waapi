<script setup>
const rhinos = ref(null);

let animation;

onMounted(() => {
  animation = rhinos.value?.animate(
    [
        { transform: 'translateX(-70vw)' },
        { transform: 'translateX(70vw)' },
    ],
    { 
        duration: 1500,
        iterations: Infinity,
        ease: 'ease-in',
    }
  );
  animation.pause();
});

function play() {
  animation.play();
}
function pause() {
  animation.pause();
}
function reverse() {
  animation.reverse();
}
</script>

<template>
  <div>
    <div ref="rhinos" class="w-80 h-auto mb-5"><Rhinos /></div>
    <div class="flex gap-5">
        <button class="btn" @click="play">Play</button>
        <button class="btn" @click="pause">Pause</button>
        <button class="btn" @click="reverse">inverser</button>
    </div>
  </div>
</template>

<style lang="css">
.btn {
    @apply px-4 py-2 text-tealight font-semibold transition relative z-10 border border-tealight rounded-lg;
}
</style>