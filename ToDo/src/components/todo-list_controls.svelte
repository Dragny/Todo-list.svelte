<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let inputValue = '';
	function onCkick() {
		if (inputValue.length) {
			dispatch('add', { text: inputValue });
			inputValue = '';
		}
	}
</script>

<div class="todo-list_controls">
	<input class="todo-list_input" type="text" bind:value={inputValue} />
	<button class="todo-list_btn" on:click={onCkick}>Добавить</button>
</div>

<style>
	.todo-list_controls {
		display: grid;
		grid-template-columns: 70% 30%;
	}
	.todo-list_input {
		border: none;
		border-radius: 15px 0 0 15px;
		padding: 20px 10px;
	}
	.todo-list_btn {
		background: #fbcc28;
		border-radius: 0 15px 15px 0;
		border: 0;
	}
</style>
