<script lang="ts">
	import Icon from './_components/icon.svelte';

	let game = new Array(9);

	let turn = 'x';

	function click(e: MouseEvent) {
		const { attributes } = <HTMLDivElement>e.target;
		const key: string = attributes.getNamedItem('data-key').nodeValue;

		game[key] = turn;
		turn = turn === 'x' ? 'o' : 'x';
	}
</script>

<div class="board">
	{#each game as slot, index}
		<div
			id="cell{index}"
			class:x={slot === 'x'}
			class:o={slot === 'o'}
			data-key={index}
			on:click={click}
		>
			{#if slot}
				<Icon size="xlg" name={slot === 'x' ? 'cross' : 'circle'} />
			{/if}
		</div>
	{/each}
</div>

<style>
	.board {
		display: grid;
		place-items: center;
		grid-template-columns: 4rem 4rem 4rem;
		grid-template-rows: 4rem 4rem 4rem;
		align-items: stretch;
		justify-items: stretch;
		width: 100%;
		gap: 0.5rem;
	}
	.board > div {
		background-color: darkgray;
		border-radius: 1rem;
		border-bottom: 0.25rem solid black;
		display: flex;
		align-items: center;
		justify-items: center;
	}
</style>
