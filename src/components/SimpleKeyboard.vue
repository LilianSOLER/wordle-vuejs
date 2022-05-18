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
</style>
