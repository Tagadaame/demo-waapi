<script setup>
const rhinos = ref(null);

function animateRhinos() {
  rhinos.value?.animate(
    [
      { transform: 'translateX(-70vw)' },
      { transform: 'translateX(70vw)' },
    ],
    {
      delay: 1000,
      duration: 1500,
      iterations: Infinity,
      ease: 'ease-in',
    }
  );
}

onMounted(() => {
  animateRhinos();
});
</script>

<template>
  <div ref="rhinos" class="w-80 h-auto"><Rhinos /></div>
</template>
