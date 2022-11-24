<script setup lang="ts">
const props = defineProps({
	source: String,
	height: {
		type: Number,
		default: 350,
	},
});
</script>

<template>
	<iframe
		class="w-full"
		:src="
			`https://stackblitz.com/edit/` + source + `?embed=` + `1&file=index.tsx`
		"
		frameborder="0"
		:height="height"
	>
	</iframe>
</template>
