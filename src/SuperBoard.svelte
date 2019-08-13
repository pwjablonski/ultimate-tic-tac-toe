<script>
	import SubBoard from "./SubBoard.svelte"
	export let superBoard;
	export let subBoards;
	export let playableSubBoard;
</script>

<div class="superBoard">
	{#each subBoards as subBoard, i}
	  <SubBoard
			superBoardVal={superBoard[i]}
			subBoard={subBoard}
			boardNum={i}
			playableSubBoard={playableSubBoard}
			on:message
		/>
	{/each}
</div>

<style>
	.superBoard {
		height: 450px;
		width: 450px;
		display: flex;
		flex-wrap: wrap;
	}
</style>