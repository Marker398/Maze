# Maze
It is a maze only for devices that support keyboard.
<!DOCTYPE html>
<html>
<head>
    <title>Maze Game</title>
    <h1>Maze</h1>
    <h1>Controls:</h1>
    <h4>Arrow up to go upwards</h4>
    <h4>Arrow down to go downwards</h4>
    <h4>Arrow left to go left</h4>
    <h4>Arrow right to right</h4>
    <h2>*Only compatible with <strong>keyboard</strong></h2>
    <h3>Channel:</h3>
    <li><a href="https://youtu.be/6JdvE6-uweE">My Channel</a></li>
    
</head>
<style>#maze-container {
    display: grid;
    grid-template-columns: repeat(10, 50px);
    grid-template-rows: repeat(7, 50px);
    width: 500px;
    height: 1000px;
    border: 1px solid black;
}

.cell {
    border: 1px solid gray;
    box-sizing: border-box;
}

.player {
    background-color: rgb(0, 23, 128);
}

.wall {
    background-color: rgb(0, 0, 0);
}

.exit {
    background-color: red;
}

button {
    margin-top: 10px;
}
</style>
<body>
    <h1>Maze Game</h1>
    <div id="maze-container"></div>
    <button id="reset-button">Reset</button>
<script>
    document.addEventListener('DOMContentLoaded', () => {
    const mazeContainer = document.getElementById('maze-container');
    const resetButton = document.getElementById('reset-button');
   
    const maze = [
        ['#', '#', '#', '#', '#', '#', '#', '#', '#', '#'],
        ['#', ' ', ' ', ' ', '#', ' ', ' ', ' ', ' ', '#'],
        ['#', ' ', '#', ' ', '#', ' ', '#', '#', ' ', '#'],
        ['#', ' ', '#', ' ', ' ', ' ', '#', ' ', ' ', '#'],
        ['#', ' ', '#', '#', '#', '#', '#', '#', '#', '#'],
        ['#', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '#'],
        ['#', '#', ' ', '#', '#', '#', '#', '#', '#', '#'],
        ['#', ' ', ' ', ' ', '#', ' ', ' ', ' ', ' ', '#'],
        ['#', '#', '#', ' ', '#', ' ', '#', '#', ' ', '#'],
        ['#', ' ', '#', ' ', ' ', ' ', '#', ' ', ' ', '#'],
        ['#', ' ', '#', '#', '#', '#', '#', ' ', '#', '#'],
        ['#', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', '#'],
        ['#', '#', '#', '#', '#', '#', '#', '#', ' ', '#'],
        ['#', ' ', ' ', ' ', '#', ' ', ' ', ' ', ' ', '#'],
        ['#', ' ', '#', ' ', '#', ' ', '#', '#', '#', '#'],
        ['#', ' ', '#', ' ', ' ', ' ', '#', 'E', '#', '#'],
        ['#', ' ', '#', '#', '#', '#', '#', ' ', ' ', '#'],
        ['#', ' ', ' ', '#', ' ', ' ', ' ', '#', ' ', '#'],
        ['#', '#', ' ', ' ', ' ', '#', ' ', ' ', ' ', '#'],
        ['#', '#', '#', '#', '#', '#', '#', '#', '#', '#']
    ];

    let playerPosition = { x: 1, y: 1 };

    function renderMaze() {
        mazeContainer.innerHTML = '';

        for (let i = 0; i < maze.length; i++) {
            for (let j = 0; j < maze[i].length; j++) {
                const cell = document.createElement('div');
                cell.className = 'cell';

                if (maze[i][j] === '#') {
                    cell.classList.add('wall');
                } else if (maze[i][j] === ' ') {
                    cell.classList.add('path');
                } else if (maze[i][j] === 'E') {
                    cell.classList.add('exit');
                }

                if (i === playerPosition.y && j === playerPosition.x) {
                    cell.classList.add('player');
                }

                mazeContainer.appendChild(cell);
            }
        }
    }

    function movePlayer(x, y) {
        if (maze[playerPosition.y + y][playerPosition.x + x] !== '#') {
            playerPosition.x += x;
            playerPosition.y += y;
            renderMaze();

            if (maze[playerPosition.y][playerPosition.x] === 'E') {
                alert('Congratulations, you\'ve reached the exit!');
            }
        }
    }

    document.addEventListener('keydown', (event) => {
        if (event.key === 'ArrowUp') {
            movePlayer(0, -1);
        } else if (event.key === 'ArrowDown') {
            movePlayer(0, 1);
        } else if (event.key === 'ArrowLeft') {
            movePlayer(-1, 0);
        } else if (event.key === 'ArrowRight') {
            movePlayer(1, 0);
        }
    });
    
    resetButton.addEventListener('click', () => {
        playerPosition = { x: 1, y: 1 };
        renderMaze();
    });

    renderMaze();
});</script>
</body>
</html>
