<script>
	export let id;
	export let text;
	export let isDone;
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
</script>

<div class="todo-list_item" class:todo-list_item-done={isDone}>
	<input type="checkbox" on:change={dispatch('change', { id })} checked={isDone} />
	<span class="todo-list_item-text">{text}</span>
	<button class="todo-list_item-btn" on:click={dispatch('remove', { id })}>Удалить</button>
</div>

<style>
	.todo-list_item {
		background: #ffebeb;
		border-radius: 10px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 10px;
		padding: 20px;
	}
	.todo-list_item-done {
		background: #ebffed;
	}
	.todo-list_item-done .todo-list_item-text {
		text-decoration: line-through;
	}
	.todo-list_item-text {
		flex-grow: 1;
	}
	.todo-list_item-btn {
		border: none;
		border-radius: 10px;
		background-color: #dc6bff;
		min-width: 100px;
		height: 30px;
	}
</style>
