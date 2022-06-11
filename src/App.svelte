<script>
	let todos = [
		{ done: false, text: 'finish Svelte tutorial' },
		{ done: false, text: 'build an app' },
		{ done: false, text: 'world domination' }
	];

	function add() {
		todos = todos.concat({ done: false, text: '' });
	}

	function clear() {
		todos = todos.filter(t => !t.done);
	}

	$: remaining = todos.filter(t => !t.done).length;
	$: count = todos.length;
</script>

<main>
	<h1>TODO</h1>

	{#each todos as todo}
		<div class:done={todo.done}>
			<input
				type="checkbox"
				bind:checked={todo.done}
			>

			<input
				placeholder="What needs to be done?"
				bind:value={todo.text}
			>
		</div>
	{/each}

	{#if todos.length > 0 }
		<p>{remaining} of {count} remaining</p>
	{:else}
		<p>You completed all todos!</p>
	{/if}

	<button on:click={add}>
		Add new
	</button>

	<button on:click={clear}>
		Clear completed
	</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	.done {
		opacity: 0.4;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>