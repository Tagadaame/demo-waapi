<script setup>
const svgScroll = ref(null);

const sections = ref([]);
const observer = ref(null);

function animateSvgScroll() {
    svgScroll.value?.animate(
        [
        { transform: 'translateY(-1vh)' },
        { transform: 'translateY(1vh)' },
        ],
        {
        delay: 1000,
        duration: 500,
        iterations: Infinity,
        ease: 'ease-in',
        }
    );
}

onMounted(() => {
  animateSvgScroll();
  sections.value = document.querySelectorAll(".section");

  observer.value = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const titles = entry.target.querySelectorAll("h1, hr, h2");
        titles.forEach((title, index) => {
          title.animate(
            [
              { transform: "translateX(100px)", opacity: 0 },
              { transform: "translateX(0)", opacity: 1 },
            ],
            {
              duration: 600,
              easing: "ease-out",
              delay: index * 150, 
              fill: "forwards",
            }
          );
        });
        observer.value.unobserve(entry.target); 
      }
    });
  }, { threshold: 0.2 });

  sections.value.forEach((section) => observer.value.observe(section));
});

onUnmounted(() => {
  if (observer.value) {
    observer.value.disconnect();
  }
});
</script>

<template>
  <div class="relative h-full w-full overflow-y-auto transition-all duration-700">
    <div class="relative z-10 flex flex-col items-center gap-10 py-20">
        <div class="h-[50vh] gap-4 flex flex-col items-center justify-center uppercase text-tealight font-bold">
            <span>scroll</span>
            <svg ref="svgScroll" width="50px" height="50px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill="#8eb5ae" d="M12 5L12.5303 4.46967C12.2374 4.17678 11.7626 4.17678 11.4697 4.46967L12 5ZM12 13L11.4697 13.5303C11.7626 13.8232 12.2374 13.8232 12.5303 13.5303L12 13ZM9.46967 6.46967C9.17678 6.76256 9.17678 7.23744 9.46967 7.53033C9.76256 7.82322 10.2374 7.82322 10.5303 7.53033L9.46967 6.46967ZM13.4697 7.53033C13.7626 7.82322 14.2374 7.82322 14.5303 7.53033C14.8232 7.23744 14.8232 6.76256 14.5303 6.46967L13.4697 7.53033ZM10.5303 10.4697C10.2374 10.1768 9.76256 10.1768 9.46967 10.4697C9.17678 10.7626 9.17678 11.2374 9.46967 11.5303L10.5303 10.4697ZM14.5303 11.5303C14.8232 11.2374 14.8232 10.7626 14.5303 10.4697C14.2374 10.1768 13.7626 10.1768 13.4697 10.4697L14.5303 11.5303ZM3.25 10V14H4.75V10H3.25ZM20.75 14V10H19.25V14H20.75ZM11.25 5V13H12.75V5H11.25ZM11.4697 4.46967L9.46967 6.46967L10.5303 7.53033L12.5303 5.53033L11.4697 4.46967ZM11.4697 5.53033L13.4697 7.53033L14.5303 6.46967L12.5303 4.46967L11.4697 5.53033ZM12.5303 12.4697L10.5303 10.4697L9.46967 11.5303L11.4697 13.5303L12.5303 12.4697ZM12.5303 13.5303L14.5303 11.5303L13.4697 10.4697L11.4697 12.4697L12.5303 13.5303ZM20.75 10C20.75 5.16751 16.8325 1.25 12 1.25V2.75C16.0041 2.75 19.25 5.99594 19.25 10H20.75ZM12 22.75C16.8325 22.75 20.75 18.8325 20.75 14H19.25C19.25 18.0041 16.0041 21.25 12 21.25V22.75ZM3.25 14C3.25 18.8325 7.16751 22.75 12 22.75V21.25C7.99594 21.25 4.75 18.0041 4.75 14H3.25ZM4.75 10C4.75 5.99594 7.99594 2.75 12 2.75V1.25C7.16751 1.25 3.25 5.16751 3.25 10H4.75Z" />
            </svg>
        </div>
      <section
        v-for="i in 7"
        :key="i"
        class="section w-4/5 h-screen flex flex-col text-tealight items-start justify-center bg-white rounded-xl px-64"
      >
        <h1 style=" transform: translateX(100px); opacity: 0 " class="text-3xl font-bold uppercase">Ceci est titre {{ i }}</h1>
        <hr style=" transform: translateX(100px); opacity: 0 " class="w-20 my-10 h-3 bg-beige">
        <h2 style=" transform: translateX(100px); opacity: 0 " class="text-lg font-light">Ceci est un sous titre {{ i  }}</h2>
      </section>
    </div>
  </div>
</template>
