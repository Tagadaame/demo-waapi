<script setup>
const rhinos = ref(null);

function animateRhinos() {
  rhinos.value?.animate(
    [
      { transform: 'translateX(-100vw)' },
      { transform: 'translateX(100vw)' },
    ],
    {
      duration: 4000,
      iterations: Infinity,
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
