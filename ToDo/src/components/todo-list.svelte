<script>
	import { onMount } from 'svelte';
	import TodoListControls from './todo-list_controls.svelte';
	import TodoListItem from './todo-list_item.svelte';

	let items = [];
	let id = 0;

	onMount(() => {
		if (localStorage.key('items')) {
			items = JSON.parse(localStorage.getItem('items'));
		}
		if (items.length) {
			items.forEach((i) => {
				if (id < i.id) {
					id = i.id;
				}
			});
			id++;
		}
	});

	function onChangeStatus(event) {
		const item = items.find((i) => i.id === event.detail.id);
		item.isDone = !item.isDone;
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}

	function onAddItem(event) {
		const item = {
			id: id++,
			text: event.detail.text,
			isDone: false
		};
		items.push(item);
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}

	function onDeleteItem(event) {
		const idx = items.findIndex((i) => i.id === event.detail.id);
		items.splice(idx, 1);
		items = items;
		localStorage.setItem('items', JSON.stringify(items));
	}
</script>

<div class="todo-list">
	<TodoListControls on:add={onAddItem} />
	<div class="todo-list_field">
		{#each items as item}
			<TodoListItem
				id={item.id}
				text={item.text}
				isDone={item.isDone}
				on:change={onChangeStatus}
				on:remove={onDeleteItem}
			/>
		{/each}
	</div>
</div>

<style>
	.todo-list {
		background: #e6e6e6;
		border-radius: 15px;
		height: 80%;
		width: 700px;
		padding: 40px 60px;
		display: flex;
		flex-direction: column;
		gap: 20px;
	}
	.todo-list_field {
		background: #ffffff;
		border-radius: 15px;
		display: flex;
		flex-direction: column;
		gap: 10px;
		overflow-y: auto;
		flex-grow: 1;
		padding: 20px;
	}
</style>
