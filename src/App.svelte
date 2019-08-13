<script>
	import SuperBoard from "./SuperBoard.svelte"
	let subBoards;
	let superBoard;
	let currentPlayer;
	let playableSubBoard;
	setBoard()
	
	function setBoard(){
		subBoards = [];
		superBoard = [];
		playableSubBoard = -1
		currentPlayer = "O"
		for (let i = 0; i < 9; i ++) {
			subBoards.push([]);
			for (let j = 0; j < 9; j ++) {
				subBoards[i].push("");
			}
		}

		for (let i = 0; i < 9; i ++) {
			superBoard.push("");
		}
	}
	
	function updatePlayableSubBoard(i){
		if(superBoard[i] === "") {
			playableSubBoard = i
		} else {
			playableSubBoard = -1
		}
	}
	
	function updatePlayer(){
		if (currentPlayer === "X") {
		  currentPlayer = "O"
		} else {
			currentPlayer = "X"
		}
	}

	function checkWin(bo){
		for(let i = 0; i < 3; i ++){
			if (
				bo[i*3 +0] === currentPlayer &&
				bo[i*3 +1] === currentPlayer &&
				bo[i*3 +2] === currentPlayer){
				return true;
			}
		}
		for(let i = 0; i < 3; i ++){
			if (
				bo[i] === currentPlayer &&
				bo[i+3] === currentPlayer &&
				bo[i+6] === currentPlayer){
				return true;
			}
		}
		if (bo[0] === currentPlayer && bo[4] === currentPlayer && bo[8] === currentPlayer){
			 return true
		}
		if (bo[2] === currentPlayer && bo[4] === currentPlayer && bo[6] === currentPlayer){
			 return true
		}
		return false
	}
	
	function handleClick(event){
		const {boardNum, cellNum} = event.detail
		if(boardNum === playableSubBoard || playableSubBoard === -1){
			 if(subBoards[boardNum][cellNum] === "" && superBoard[boardNum] === ""){
				subBoards[boardNum][cellNum] = currentPlayer
				subBoards = subBoards
				if(checkWin(subBoards[boardNum])){
					superBoard[boardNum] = currentPlayer
					superBoard = superBoard
				}
				if(checkWin(superBoard)){
					alert(`${currentPlayer} wins!`)
					setBoard();
					return
				}
				updatePlayableSubBoard(cellNum);
				updatePlayer();
			}
		}
	}
</script>

<div class="app">
	<h1>Ultimate Tic Tac Toe!</h1>
	<p>Current Player: {currentPlayer}</p>

	<SuperBoard
		superBoard={superBoard}
		subBoards={subBoards}
		playableSubBoard={playableSubBoard}
		on:message={handleClick}
	/>
</div>


<style>
	.app {
		display:flex;
		flex-direction:column;
		align-items:center;
	}
</style>