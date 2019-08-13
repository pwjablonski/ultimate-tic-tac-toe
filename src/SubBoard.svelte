<script>
	import Cell from "./Cell.svelte"	
	export let subBoard;
	export let boardNum;
	export let playableSubBoard;
	export let superBoardVal;
	$: isSolved = superBoardVal !== ''
	$: isPlayable = playableSubBoard === -1 || playableSubBoard === boardNum
</script>

<div class="subBoardContainer">
	{#if isSolved}
		<div class="subBoardOverlay {superBoardVal}">
			{superBoardVal}
		</div>
	{/if}
	<div class="subBoard {isPlayable ? 'active' : null}">
		{#each subBoard as cellVal, j}
			<Cell
				cellVal={cellVal}
				boardNum={boardNum}
				cellNum={j}
				on:message
			/>
		{/each}
	</div>
</div>

<style>
	.subBoardContainer {
		width: 32%;
		height: 32%;
		position:relative
	}
	.subBoard {
		display: flex;
		flex-wrap:wrap;
        justify-content: center;
        align-items: center;
		width: 100%;
		height: 100%;
	}
	.subBoard.active{
		border: 1px solid red;
	}
	.subBoardOverlay{
		position:absolute;
		font-size:5em;
		top: 30px;
		left: 45px;
	}
	.subBoardOverlay.X {
		color: blue;
	}
	.subBoardOverlay.O {
		color: red;
	}
</style>