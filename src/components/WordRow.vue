<script setup lang="ts">
import LetterBox from "./LetterBox.vue";
import { ref, watch } from "vue";

const props = defineProps({
	value: String,
	solutions: String,
	submitted: Boolean,
});

const colors = ref(["", "", "", "", ""]);

watch(
	() => props.submitted,
	async (submitted, prevSubmited) => {
		if (props.submitted) {
			let s = props.solutions;
			let v = props.value;

			let tmp = ["gray", "gray", "gray", "gray", "gray"];
			let letterPool = [];
			for (let i = 0; i < s.length; i++) {
				if (s.charAt(i) == v.charAt(i)) {
					tmp[i] = "green";
				} else {
					letterPool.push(s.charAt(i));
				}
			}
			for (let i = 0; i < 5; i++) {
				if (tmp[i] == "gray") {
					let index = s.indexOf(letterPool[i]);
					if (index != -1) {
						letterPool.splice(index, 1);
						tmp[index] = "yellow";
					}
				}
				colors.value[i] = tmp[i];
				await new Promise((resolve) => setTimeout(resolve, 500));
			}
		}
	}
);
</script>

<template>
	<div class="grid max-w-xs grid-cols-5 gap-1 mx-auto mb-1">
		<LetterBox
			v-for="i in 5"
			:key="i"
			:letter="value[i - 1]"
			:color="colors[i - 1]"
		/>
	</div>
</template>

<style scoped></style>
