<script setup lang="ts">
import SimpleKeyboard from "./components/SimpleKeyboard.vue";
import { onMounted } from "vue";

const handleInput = (button) => {
	console.log(button);
};

onMounted(() => {
	window.addEventListener("keyup", (e) => {
		e.preventDefault();
		let key =
			e.key == "enter"
				? "{enter}"
				: e.key == "backspace"
				? "{bksp}"
				: e.key.toLowerCase();
		handleInput(key);
	});
});
</script>

<template>
	<div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
		<simple-keyboard @onKeyPress="handleInput" />
	</div>
</template>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
