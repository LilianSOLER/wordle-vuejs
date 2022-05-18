<script setup lang="ts">
import SimpleKeyboard from "./components/SimpleKeyboard.vue";
import WordRow from "./components/WordRow.vue";
import { reactive, onMounted } from "vue";

const state = reactive({
	solution: "books",
	guesses: ["", "", "", "", ""],
	currentGuessIndex: 0,
});

const handleInput = (key) => {
	const currentGuess = state.guesses[state.currentGuessIndex];

	if (key == "{enter}") {
		// Submit the current guess
	} else if (state.currentGuessIndex >= 6) {
		return;
	} else if (key == "{bksp}") {
		state.guesses[state.currentGuessIndex] = currentGuess.slice(0, -1); // remove last character
	} else if (currentGuess.length < 5) {
		if (/[a-zA-Z]/.test(key)) {
			state.guesses[state.currentGuessIndex] += key;
		}
	}
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
		<div>
			<WordRow
				v-for="(guesses, i) in state.guesses"
				:key="i"
				:value="guesses"
				:solutions="state.solution"
				:submitted="i < state.currentGuessIndex"
			/>
		</div>
		<SimpleKeyboard @onKeyPress="handleInput" />
	</div>
</template>

<style></style>
