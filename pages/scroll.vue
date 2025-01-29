<script setup>
    const sections = ref([]);
    const observer = ref(null);
    const container = ref(null);

    const colors = ["#064259", "#026C80", "#8EB5AE", "#eaac80", "#df5C3E"];
    const bgColor = ref(colors[0]);

    onMounted(() => {
    sections.value = document.querySelectorAll(".section");

    observer.value = new IntersectionObserver(
        (entries) => {
        entries.forEach((entry) => {
            if (entry.isIntersecting) {
            bgColor.value = entry.target.dataset.color; 
            }
        });
        },
        { threshold: 0.6, root: container.value }
    );
    sections.value.forEach((section) => observer.value.observe(section));
    });

    onUnmounted(() => {
    if (observer.value) {
        observer.value.disconnect();
    }
    });
</script>

<template>
  <div ref="container" class="relative h-full w-full overflow-y-auto transition-all duration-700" 
    :style="{ backgroundColor: bgColor }">
    <div class="relative z-10 flex flex-col items-center gap-10 py-20">
      <section
        v-for="(color, index) in colors"
        :key="index"
        class="section w-4/5 h-screen flex items-center justify-center text-3xl font-bold border bg-white transition-all duration-300 rounded-xl"
        :data-color="color"
        :style="{ color: color }"
      >
        Section {{ index + 1 }}
      </section>
    </div>
  </div>
</template>

