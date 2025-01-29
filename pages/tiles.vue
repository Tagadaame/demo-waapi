
<script setup>

const tiles = ref([]);

const removeTile = (tile) => {
  tile.animate(
	[
	  { opacity: 1, transform: "scale(1)" },
	  { opacity: 0, transform: "scale(0.8)" },
	],
	{
	  duration: 300,
	  easing: "ease-out",
	}
  ).onfinish = () => {
	tile.style.visibility = "hidden";
  };
};

function resetTiles() {
  tiles.value.forEach((tile) => {
		tile.animate(
		[
			{ opacity: 0, transform: "scale(0.8)" },
			{ opacity: 1, transform: "scale(1)" },
		],
		{
			duration: 300,
			easing: "ease-out",
		}
	).onfinish = () => {
		tile.style.visibility = "visible";
	};
  });
}

onMounted(() => {
  tiles.value = document.querySelectorAll(".tile");
  tiles.value.forEach((tile) => {
	tile.addEventListener("mouseenter", () => removeTile(tile));
  });
});

</script>

<template>
  <div class="flex flex-col items-center gap-4 relative">
	<button @click="resetTiles" class="px-4 py-2 text-tealight font-semibold transition hover:bg-white relative z-10 border border-tealight rounded-lg">
	  Reset
	</button>

	<!-- Grille de tuiles -->
	<div class="grid grid-cols-10 grid-rows-10 w-[400px] h-[400px] gap-1 relative z-20">
	  <div
		v-for="n in 100"
		:key="n"
		class="tile w-full h-full bg-tealight transition-opacity duration-300 cursor-pointer"
	  ></div>
	</div>
	<span class="z-0 absolute top-0 left-0 right-0 bottom-0 flex items-center justify-center">
		<Rhinos class="w-1/2 m-auto opacity-20" />
	</span> 
  </div>
</template>



