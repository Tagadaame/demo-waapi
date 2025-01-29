
<script setup>

const buttonRef = ref(null);
const added = ref(false);

const animateButton = () => {
  if (!buttonRef.value) return;
  const animation = buttonRef.value.animate(
    [
      { transform: "scale(1)", offset: 0 },
      { transform: "scale(1.1)", offset: 0.3 },
      { transform: "scale(0.9)", offset: 0.6 },
      { transform: "scale(1)", offset: 1 },
    ],
    {
      duration: 300,
      easing: "ease-out",
    }
  );

  animation.onfinish = () => {
    added.value = true;
    setTimeout(() => {
      added.value = false;
    }, 1500);
  };
};
</script>

<template>
  <button
    ref="buttonRef"
    @click="animateButton"
    class="relative px-6 py-3 text-white font-semibold rounded-lg transition-all duration-300 bg-tealight hover:bg-tealight active:scale-95 flex items-center gap-2"
  >
    <span v-if="!added">Ajouter au panier</span>
    <span v-else>Ajouté !</span>
  </button>
</template>
