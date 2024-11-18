<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tic Tac Toe Game</title>
<style>
    /* Body Style */
    body {
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        height: 100vh;
        background: linear-gradient(to right, #ff7e5f, #feb47b);
        margin: 0;
    }

    /* Game Title */
    h1 {
        font-size: 3rem;
        color: #fff;
        text-align: center;
        margin-bottom: 5px;
    }

    .subtitle {
        font-size: 1.5rem;
        color: #fff;
        font-family: 'Courier New', Courier, monospace;
        margin-bottom: 20px;
    }

    /* Game Container */
    .game-container {
        background: #fff;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
        text-align: center;
    }

    /* Game Board */
    .board {
        display: grid;
        grid-template-columns: repeat(3, 100px);
        grid-template-rows: repeat(3, 100px);
        gap: 5px;
        margin: 20px 0;
    }

    .cell {
        width: 100px;
        height: 100px;
        background-color: #f0f8ff;
        border: 3px solid #000;
        font-size: 2rem;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        border-radius: 10px;
    }

    .cell:hover {
        background-color: #e0e0e0;
    }

    .X {
        color: red;
        font-weight: bold;
    }

    .O {
        color: blue;
        font-weight: bold;
    }

    /* Options and Scoreboard */
    #status {
        font-size: 1.2rem;
        margin-bottom: 10px;
        font-weight: bold;
    }

    .scoreboard {
        display: flex;
        justify-content: space-between;
        margin: 10px 0;
    }

    .scoreboard div {
        font-size: 1.2rem;
        color: #333;
    }

    .options {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }

    .options button {
        padding: 10px 20px;
        cursor: pointer;
        border: none;
        background-color: #ff5e57;
        color: #fff;
        border-radius: 5px;
        margin: 0 5px;
    }

    .options button:hover {
        background-color: #ff7e5f;
    }
</style>
</head>
<body>
    <h1>Tic Tac Toe Game</h1>
    <div class="subtitle">by Viratiansouvik</div>
    <div class="game-container">
        <div class="options">
            <button id="easy">Easy</button>
            <button id="medium">Medium</button>
            <button id="hard">Hard</button>
        </div>
        <div class="scoreboard">
            <div>Player X Score: <span id="xScore">0</span></div>
            <div>Player O Score: <span id="oScore">0</span></div>
        </div>
        <div id="status">Player X's Turn</div>
        <div class="board" id="board">
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
            <div class="cell" data-cell></div>
        </div>
        <button id="restartButton">Restart Game</button>
    </div>

<script>
    const board = document.getElementById('board');
    const statusDisplay = document.getElementById('status');
    const cells = document.querySelectorAll('[data-cell]');
    const restartButton = document.getElementById('restartButton');
    const xScoreDisplay = document.getElementById('xScore');
    const oScoreDisplay = document.getElementById('oScore');
    const easyButton = document.getElementById('easy');
    const mediumButton = document.getElementById('medium');
    const hardButton = document.getElementById('hard');

    let currentPlayer = 'X';
    let xScore = 0;
    let oScore = 0;
    let gameActive = true;
    const winningCombinations = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ];

    function checkWin() {
        return winningCombinations.some(combination => 
            combination.every(index => cells[index].textContent === currentPlayer));
    }

    function handleClick(e) {
        const cell = e.target;
        if (cell.textContent || !gameActive) return;
        cell.textContent = currentPlayer;
        cell.classList.add(currentPlayer);
        if (checkWin()) {
            gameActive = false;
            currentPlayer === 'X' ? xScore++ : oScore++;
            xScoreDisplay.textContent = xScore;
            oScoreDisplay.textContent = oScore;
            statusDisplay.textContent = `Player ${currentPlayer} Wins!`;
            setTimeout(() => alert(`Player ${currentPlayer} Wins!`), 100);
        } else if ([...cells].every(cell => cell.textContent)) {
            statusDisplay.textContent = "Draw!";
        } else {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusDisplay.textContent = `Player ${currentPlayer}'s Turn`;
        }
    }

    function restartGame() {
        cells.forEach(cell => (cell.textContent = ''));
        currentPlayer = 'X';
        gameActive = true;
        statusDisplay.textContent = "Player X's Turn";
    }

    restartButton.addEventListener('click', restartGame);
    cells.forEach(cell => cell.addEventListener('click', handleClick));
</script>
</body>
</html>
