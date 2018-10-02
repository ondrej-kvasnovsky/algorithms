# A\* Search Algorithm

A\* Search algorithm is extension of Dijkstra algorithm to find shortest path between two points in a graph using heuristics to guid the search \(heuristic is distance from start to the current point and distance from current point to the last one\).

Nice [explanation of A\* search algorithm](https://www.youtube.com/watch?v=aKYlikFAV4k) with visualization. Here is the code that does not do any visuals but is just implements what was done in that video in JavaScript. 

```
class Grid {
  constructor(cols, rows) {
    this.cols = cols;
    this.rows = rows;
    this.grid = new Array(cols);
    this.setup();
    this.openSet = [];
    this.closedSet = [];
  }

  setup() {
    for (let i = 0; i < this.cols; i++) {
      this.grid[i] = new Array(this.rows);
    }
    for (let i = 0; i < this.cols; i++) {
      for (let j = 0; j < this.rows; j++) {
        this.grid[i][j] = new Spot(i, j);
      }
    }
    for (let i = 0; i < this.cols; i++) {
      for (let j = 0; j < this.rows; j++) {
        this.grid[i][j].addNeighbors(this);
      }
    }
  }

  find(i1, j1, i2, j2) {
    // cleanup to enable a new search over the same array
    this.closedSet = [];
    this.openSet = [];
    for (let i = 0; i < this.cols; i++) {
      for (let j = 0; j < this.rows; j++) {
        this.grid[i][j].f = 0;
        this.grid[i][j].g = 0;
        this.grid[i][j].h = 0;
        this.grid[i][j].previous = undefined;
      }
    }

    this.start = this.grid[i1][j1];
    this.end = this.grid[i2][j2];
    this.openSet.push(this.start);
    while (this.openSet.length > 0) {
      let lowestIndex = 0;
      for (let i = 0; i < this.openSet.length; i++) {
        if (this.openSet[i].f < this.openSet[lowestIndex].f)
          lowestIndex = i;
      }
      var current = this.openSet[lowestIndex];
      if (current === this.end) {
        console.log("Done");
        let temp = current;
        const path = []
        path.push(temp);
        while (temp.previous) {
          path.push(temp.previous);
          temp = temp.previous;
        }
        return path;
      }

      // remove from open set when current exists
      for (let i = this.openSet.length - 1; i >= 0; i--) {
        if (this.openSet[i] === current)
          this.openSet.splice(i, 1);
      }
      this.closedSet.push(current);

      // add candidates where to go
      let neighbors = current.neighbors;
      for (let i = 0; i < neighbors.length; i++) {
        let neighbor = neighbors[i];
        if (!this.closedSet.includes(neighbor) && !neighbor.wall) {
          let tempG = current.g + 1;
          let foundNewPath = false;
          if (this.openSet.includes(neighbor)) {
            if (tempG < neighbor.g) { // we found better shorter distance to the end
              neighbor.g = tempG;
              foundNewPath = true;
            }
          } else {
            neighbor.g = tempG;
            foundNewPath = true;
            this.openSet.push(neighbor);
          }
          if (foundNewPath) {
            neighbor.h = this.heuristic(neighbor, this.end);
            neighbor.f = neighbor.g + neighbor.h;
            neighbor.previous = current;
          }
        }
      }
    }
  }

  heuristic(a, b) {
    let distance = Math.sqrt(Math.pow(b.i - a.i, 2) + Math.pow(b.j - a.j, 2));
    return distance;
  }
}

class Spot {
  constructor(i, j) {
    this.i = i;
    this.j = j;
    this.f = 0;
    this.g = 0; // amount of time, cost, it takes from 0
    this.h = 0; // amount of time, cost, it takes to the end
    this.neighbors = [];
    this.previous = undefined;
    this.wall = false;
    // if (Math.random(1) < 0.3) {
    //   this.wall = true;
    // }
  }

  addNeighbors(grid) {
    const i = this.i;
    const j = this.j;
    const cols = grid.cols;
    const rows = grid.rows;

    if (i < cols - 1)
      this.neighbors.push(grid.grid[i + 1][j]);
    if (i > 0)
      this.neighbors.push(grid.grid[i - 1][j]);
    if (j < rows - 1)
      this.neighbors.push(grid.grid[i][j + 1]);
    if (j > 0)
      this.neighbors.push(grid.grid[i][j - 1]);
    // add diagonal neighbors
    if (i > 0 && j > 0)
      this.neighbors.push(grid.grid[i - 1][j - 1]);
    if (i < cols - 1 && j > 0)
      this.neighbors.push(grid.grid[i + 1][j - 1]);
    if (i > 0 && j < rows - 1)
      this.neighbors.push(grid.grid[i - 1][j + 1]);
    if (i < cols - 1 && j < rows - 1)
      this.neighbors.push(grid.grid[i + 1][j + 1]);
  }
}

const grid = new Grid(10, 10);
const path = grid.find(0, 0, 0, 4);

for (const p of path)
  console.log(p.i, p.j);

```



