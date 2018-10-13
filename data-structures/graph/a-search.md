# A\* Search Algorithm

A\* Search algorithm is extension of Dijkstra algorithm to find shortest path between two points in a graph using heuristics to guid the search \(heuristic is distance from start to the current point and distance from current point to the last one\).

![](/assets/Screen Shot 2018-10-12 at 11.13.58 PM.png)

Here is the implementation of the algorithm above, using p5 library.

```
index.html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>p5.js example</title>
    <style> body {padding: 10; margin: 10;} </style>
    <script src="./p5.min.js"></script>
    <script src="./p5.dom.min.js"></script>
    <script src="./p5.sound.min.js"></script>
    <script src="./sketch.js"></script>
  </head>
  <body>
  </body>
</html>

sketch.js
// https://github.com/CodingTrain/AStar/blob/master/sketch.js
let cols = 25;
let rows = 25;
let grid = new Array(cols);
let squareSize = 10;
let a = { x: 0, y: 0 }
let b = { x: 0, y: 1 }
let aTo = { x: 0, y: 0 }
let bTo = { x: 0, y: 1 }

let openSet = [];
let closedSet = [];
let start;
let end;
let path = [];

function Spot(i, j) {
    this.i = i;
    this.j = j;
    this.f = 0;
    this.g = 0; // amount of time, cost, it takes from 0
    this.h = 0; // amount of time, cost, it takes to the end
    this.neighbors = [];
    this.previous = undefined;
    this.wall = false;
    if (random(1) < 0.3) {
        this.wall = true;
    }
    this.show = function(color) {
        fill(color);
        // noStroke();
        if (this.wall) {
            fill(0);
        }
        rect(this.i * squareSize, this.j * squareSize, squareSize, squareSize);
    }
    this.addNeighbors = function(grid) {
        const i = this.i;
        const j = this.j;
        if (i < cols - 1)
            this.neighbors.push(grid[i + 1][j]);
        if (i > 0)
            this.neighbors.push(grid[i - 1][j]);
        if (j < rows - 1)
            this.neighbors.push(grid[i][j + 1]);
        if (j > 0)
            this.neighbors.push(grid[i][j - 1]);

        if (i > 0 && j > 0)
            this.neighbors.push(grid[i - 1][j - 1]);
        if (i < cols - 1 && j > 0)
            this.neighbors.push(grid[i + 1][j - 1]);
        if (i > 0 && j < rows - 1)
            this.neighbors.push(grid[i - 1][j + 1]);
        if (i < cols - 1 && j < rows - 1)
            this.neighbors.push(grid[i + 1][j + 1]);
    }
}

function setup() {
      createCanvas(500, 500);
      frameRate(10);
      for (let i = 0; i < cols; i++) {
        grid[i] = new Array(rows);
    }
    for (let i = 0; i < cols; i++) {
        for (let j = 0; j < rows ; j++) {
            grid[i][j] = new Spot(i, j);
        }
    }
    for (let i = 0; i < cols; i++) {
        for (let j = 0; j < rows; j++) {
            grid[i][j].addNeighbors(grid);
        }
    }

    start = grid[cols - 1][rows - 1];
    end = grid[0][0];
    start.wall = false;
    end.wall = false;

    openSet.push(start);
}

function draw() {
    if (openSet.length > 0) {
        let lowestIndex = 0;
        for (let i = 0; i < openSet.length; i++) {
            if (openSet[i].f < openSet[lowestIndex].f)
                lowestIndex = i;
        }
        var current = openSet[lowestIndex];
        if (current === end) {
            console.log("Done");
            noLoop();
            // return;
        }

        // remove from open set when current exists
        for (let i = openSet.length - 1; i >= 0; i--) {
            if (openSet[i] === current) 
                openSet.splice(i, 1);
        }
        closedSet.push(current);

        // add candidates where to go
        let neighbors = current.neighbors;
        for (let i = 0; i < neighbors.length; i++) {
            let neighbor = neighbors[i];
            if (!closedSet.includes(neighbor) && !neighbor.wall) {
                let tempG = current.g + 1;
                let foundNewPath = false;
                if (openSet.includes(neighbor)) {
                    if (tempG < neighbor.g) { // we found better shorter distance to the end
                        neighbor.g = tempG;
                        foundNewPath = true;
                    }
                } else {
                    neighbor.g = tempG;
                    foundNewPath = true;
                    openSet.push(neighbor);
                }
                if (foundNewPath) {
                    neighbor.h = heuristic(neighbor, end);
                    neighbor.f = neighbor.g + neighbor.h;
                    neighbor.previous = current;    
                }
            } 
        }

    } else {
        console.log("No solution.");
        noLoop();
        // return;
        // no solution
    }
    for (let i = 0; i < cols; i++) {
        for (let j = 0; j < grid[i].length; j++) {
            grid[i][j].show(color(255));
        }
    }

    for (const closed of closedSet) {
        closed.show(color(255, 0, 0));
    }
    for (const open of openSet) {
        open.show(color(0, 255, 0));
    }

    path = [];
    let temp = current;
    path.push(temp);
    while (temp.previous) {
        path.push(temp.previous);
        temp = temp.previous;
    }
    for (const p of path) {
        p.show(color(0, 0, 255));
    }
}

function heuristic(a, b) {
    let d = dist(a.i, a.j, b.i, b.j);
    // let d = abs(a.i - b.i) + abs(a.j - b.j);
    return d;
}

function mouseClicked() {
    let x = int(mouseX / squareSize);
    let y = int(mouseY / squareSize);
    if (x < grid.length && 
        y < grid[0].length &&
        grid[x][y] != 1) {
        aTo.i = x;
        aTo.j = y;
    }
      return false;
}

function keyPressed() {

}
```

Nice [explanation of A\* search algorithm](https://www.youtube.com/watch?v=aKYlikFAV4k) with visualization. Here is the code that does not do any visuals but implements what was done in that video in JavaScript. It is naive implementation, not using priority queue.

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

Here is a modified version that uses priority queue \(implemented by [TinyQueue](https://github.com/mourner/tinyqueue/blob/master/index.js)\).

```
class TinyQueue {
  constructor(data = [], compare = defaultCompare) {
    this.data = data;
    this.length = this.data.length;
    this.compare = compare;

    if (this.length > 0) {
      for (let i = (this.length >> 1) - 1; i >= 0; i--) this._down(i);
    }
  }

  push(item) {
    this.data.push(item);
    this.length++;
    this._up(this.length - 1);
  }

  pop() {
    if (this.length === 0) return undefined;

    const top = this.data[0];
    const bottom = this.data.pop();
    this.length--;

    if (this.length > 0) {
      this.data[0] = bottom;
      this._down(0);
    }

    return top;
  }

  peek() {
    return this.data[0];
  }

  includes(i) { // O(n)
    for (const d of this.data) {
      if (d === i) return true;
    }
    return false;
  }

  _up(pos) {
    const {data, compare} = this;
    const item = data[pos];

    while (pos > 0) {
      const parent = (pos - 1) >> 1;
      const current = data[parent];
      if (compare(item, current) >= 0) break;
      data[pos] = current;
      pos = parent;
    }

    data[pos] = item;
  }

  _down(pos) {
    const {data, compare} = this;
    const halfLength = this.length >> 1;
    const item = data[pos];

    while (pos < halfLength) {
      let left = (pos << 1) + 1;
      let best = data[left];
      const right = left + 1;

      if (right < this.length && compare(data[right], best) < 0) {
        left = right;
        best = data[right];
      }
      if (compare(best, item) >= 0) break;

      data[pos] = best;
      pos = left;
    }

    data[pos] = item;
  }
}

function defaultCompare(a, b) {
  return a.f < b.f ? -1 : a.f > b.f ? 1 : 0;
}

class Grid {
  constructor(cols, rows) {
    this.cols = cols;
    this.rows = rows;
    this.grid = new Array(cols);
    this.setup();
    this.openSet = new TinyQueue();
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
    this.openSet = new TinyQueue();
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
      var current = this.openSet.pop();
      console.log(current.i, current.j);
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
            foundNewPath = true;
          }
          if (foundNewPath) {
            neighbor.h = this.heuristic(neighbor, this.end);
            neighbor.f = neighbor.g + neighbor.h;
            neighbor.g = tempG;
            neighbor.previous = current;
            this.openSet.push(neighbor);
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

Here is another example of how to use A\* algorithm to implement multi player walking game: [https://github.com/ondrej-kvasnovsky/walkers.](https://github.com/ondrej-kvasnovsky/walkers) 

