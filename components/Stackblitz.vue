<script setup lang="ts">
import { PropType } from "vue";

type STACKBLITZ_VIEW = "preview" | "view" | "default";

const props = defineProps({
	source: String,
	height: {
		type: Number,
		default: 350,
	},
	view: {
		type: String as PropType<STACKBLITZ_VIEW>,
	},
	console: Boolean,
	openFiles: {
		type: Array<string>,
		default: ["index.tsx"],
	},
});

const view = props.view ? `&view={${props.view}}` : "";
const console = props.console ? `&devToolsHeight=33` : "";
const filesString = props.openFiles
	.map((item, index) => {
		return `${index + 1}&file=${item}`;
	})
	.join("&");
</script>

<template>
	<iframe
		class="w-full"
		:src="
			`https://stackblitz.com/edit/` +
			source +
			`?embed=` +
			filesString +
			view +
			console
		"
		frameborder="0"
		:height="height"
	>
	</iframe>
</template>
