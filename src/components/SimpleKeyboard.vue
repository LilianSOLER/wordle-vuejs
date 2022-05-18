<script setup lang="ts">
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";
import { ref, onMounted } from "vue";

const emit = defineEmits(["onKeyPress"]);

const keyboard = ref(null);

const onKeyPress = (button) => {
	emit("onKeyPress", button);
};

onMounted(() => {
	keyboard.value = new Keyboard("simple-keyboard", {
		layout: {
			default: [
				"a z e r t y u i o p",
				"q s d f g h j k l",
				"{enter} w x c v b n m {bksp}",
			],
		},
		onKeyPress: onKeyPress,
	});
});
</script>

<template>
	<div class="simple-keyboard"></div>
</template>

<style scoped>
a {
	color: #42b983;
}

label {
	margin: 0 0.5em;
	font-weight: bold;
}

code {
	background-color: #eee;
	padding: 2px 4px;
	border-radius: 4px;
	color: #304455;
}
</style>
