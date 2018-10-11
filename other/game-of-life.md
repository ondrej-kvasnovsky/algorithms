# Game of Life

[Game of Life](https://en.wikipedia.org/wiki/Conway's_Game_of_Life]%28https://en.wikipedia.org/wiki/Conway's_Game_of_Life) is a system where cells can die, live or become alive based on surrounding cells.

![](/assets/Screen Shot 2018-10-08 at 9.51.23 PM.png)

Here is an implementation that is using [p5](https://p5js.org) library \(inspired by [Game of Life video](https://www.youtube.com/watch?v=FWSR_7kZuYg&vl=en)\).

```
let resolution;
let cols;
let rows;
let grid;

function setup() {
  frameRate(20);
  resolution = 5;
  createCanvas(400, 400);
  cols = width / resolution;
  rows = height / resolution;
  grid = createGrid(cols, rows);
}

let generationCount = 0;

function draw() {
  background(255);
  let next = createGrid(cols, rows);
  for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
      if (grid[i][j] === 1) { 
        fill(255, 90, generationCount);
        stroke(255, 90, generationCount);
        rect(i * resolution, j * resolution, resolution - 1, resolution - 1);
      }
      let sum = countNeighbors(grid, i, j);
      let current = grid[i][j];
      // Any live cell with fewer than two live neighbors dies, as if by underpopulation.
            // Any live cell with two or three live neighbors lives on to the next generation.
            // Any live cell with more than three live neighbors dies, as if by overpopulation.
            // Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
      if (current === 1 && sum < 2) {
         next[i][j] = 0;
      } else if (current === 1 && (sum === 2 || sum === 3)) {
         next[i][j] = 1;
      } else if (current === 1 && sum > 3) {
         next[i][j] = 0;
      } else if (current === 0 && sum == 3) {
         next[i][j] = 1;
      } else {
        // next[i][j] = current; // this should be there in order to keep the original algorithm design
        // just an experiment - any other will become 1 with 1% probability
        // try to lower this number and see how little 
        // probability is enough to keep cells alive or dead
        next[i][j] = random(1) < 0.01 ? 1 : 0;
      }
    }
  }
  generationCount++;
  grid = next;
}

function countNeighbors(grid, i, j) {
  let sum = 0;
  if (i > 0) sum += grid[i - 1][j];
  if (i < cols - 1) sum += grid[i + 1][j];
  if (j > 0) sum += grid[i][j - 1]; 
  if (j < rows - 1) sum += grid[i][j + 1];
  if (i > 0 && j > 0) sum += grid[i - 1][j - 1];  
  if (i < cols - 1 && j > 0) sum += grid[i + 1][j - 1];  
  if (i > 0 && j < rows - 1) sum += grid[i - 1][j + 1];  
  if (i < cols - 1 && j < rows - 1) sum += grid[i + 1][j + 1];  
  return sum;
}

function createGrid(cols, rows) {
  const grid = new Array(cols);
  for (let i = 0; i < cols; i++) {
    grid[i] = new Array(rows);
    for (let j = 0; j < rows; j++) {
      grid[i][j] = floor(random(0, 2));
    }
  }
  return grid;
}
```



