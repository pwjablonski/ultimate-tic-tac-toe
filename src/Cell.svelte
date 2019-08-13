<script>
	import { createEventDispatcher } from 'svelte';
	
	export let cellVal;
	export let cellNum;
	export let boardNum;
	const dispatch = createEventDispatcher();

	function cellClicked() {
		dispatch('message', {boardNum, cellNum});
	}
</script>

<div 
	class="cell {cellVal}"
	on:click={cellClicked}
>
	{cellVal}
</div>

<style>
	.cell {
		display:flex;
		justify-content:center;
		align-items:center;
		border: 1px solid black;
		width: 31%;
		height: 30%;
	}
	.cell.X {
		color: blue;
	}
	.cell.O {
		color: red;
	}
</style>