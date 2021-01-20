<script lang="ts">
  import {onMount} from 'svelte';
  type travelDirections = 'Up' | 'Down' | 'Left' | 'Right';

  let score = 0;
  let snakeHead: HTMLElement;
  let directionTravelling: travelDirections = 'Up';
  let foodBlockId: string;

  onMount(() => {
    setBlocks();
    placeFood(1);
    setStartingBlock();
    document.addEventListener('keydown', (e) => {
      handleKeyPress(e.code);
    });
    initializeTravel();
  })

  function setBlocks() {
    for (let index = 0; index < 400; index++) {
      let table = document.querySelector('#table');
      let block = document.createElement('div')
      block.id = `${index}`
      block.classList.add('square')
      table.appendChild(block)

    }
  }

  function setStartingBlock() {
    const startingBlockId = (Math.random() * 400).toFixed(0);
    const startingBlock = document.getElementById(`${startingBlockId}`)
    startingBlock.classList.add('snake');
    snakeHead = startingBlock;
  }

  function initializeTravel() {
    setInterval(() => {
      setSnakeDirection(directionTravelling);
      if (foodBlockId === snakeHead.id) {
        score++;
        const food = document.getElementById(`${foodBlockId}`);
        food.classList.add('square');
        food.classList.remove('food');
        placeFood(1);
      }
    }, 400)
  }

  function handleKeyPress(direction: string) {
    if(direction === 'ArrowUp') directionTravelling = 'Up'
    if(direction === 'ArrowDown') directionTravelling = 'Down'
    if(direction === 'ArrowLeft') directionTravelling = 'Left'
    if(direction === 'ArrowRight') directionTravelling = 'Right'
  }

  function setSnakeDirection(travelDirection: travelDirections) {
    let currentLocation = Number(snakeHead.id);
    let newCoordinate: string;
    directionTravelling = travelDirection;
    if (travelDirection === 'Up') newCoordinate = `${currentLocation - 20}`;
    if (travelDirection === 'Down') newCoordinate = `${currentLocation + 20}`;
    if (travelDirection === 'Left') newCoordinate = `${currentLocation - 1}`;
    if (travelDirection === 'Right') newCoordinate = `${currentLocation + 1}`;
    snakeHead.classList.remove('snake');
    snakeHead = document.getElementById(newCoordinate);
    snakeHead.classList.add('snake');
  }

  function placeFood(foodCount: number) {
    for (let i = 0; i < foodCount; i++) {
    const startingBlockId = (Math.random() * 400).toFixed(0);
    foodBlockId = startingBlockId;
    const startingBlock = document.getElementById(`${startingBlockId}`)
    startingBlock.classList.add('food');
    }
  }
</script>

<main>
  <div id="table">

  </div>
  <h1>{score}</h1>
</main>

<style>
  h1 {
    text-align: center;
  }
  #table {
    width: 800px;
    height: 800px;
    background-color: gray;
    display: grid;
    grid-template-columns: repeat(20, 40px);
    grid-template-rows: repeat(20, 40px);
    margin: auto;
    z-index: 0;
  }

  :global(.square) {
        width: 40px;
    height: 40px;
    background-color: black;
    border: 1px solid gray;
    z-index: 1;
  }

  :global(.snake) {
    background-color: red;
    z-index: 10;
  }

    :global(.food) {
    background-color: purple;
    z-index: 5;
  }
</style>
