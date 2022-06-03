<template>
  <div>
    <h1>TIC TAC TOE</h1>
    <h2>Player {{ player }}'s turn</h2>
    <button @click="resetBoard">RESET</button>
    <div class="area">
      <div class="row" v-for="(row, x) in board" :key="x">
        <div
          class="column"
          v-for="(col, y) in row"
          :key="y"
          @click="makeMove(x, y)"
        >
          {{ col == "X" ? "X" : col == "O" ? "O" : "" }}
        </div>
      </div>
    </div>
    <h1 v-if="winner">Player {{ winner }} is the winner</h1>
  </div>
</template>

<script>
export default {
  name: "PlayArea",
  data() {
    return {
      count: 0,
      winner: "",
      player: "X",
      board: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
    };
  },
  updated() {
    function calculateWinner(squares) {
      const list = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (let i = 0; i < list.length; i++) {
        let [a, b, c] = list[i];
        if (squares[a] === squares[b] && squares[a] === squares[c]) {
          return squares[a];
        }
      }

      return null;
    }
    this.winner = calculateWinner(this.board.flat());
  },
  methods: {

    makeMove(x, y) {
      if (this.winner) {
        return NaN;
      }
      if (this.board[x][y] != "") {
        return NaN;
      }

      this.count++;
      this.board[x][y] = this.player;
      this.player = this.player == "X" ? "O" : "X";

      if (this.count < 5) {
        var xrandom = randomX();
        var yrandom = randomX();
        while (this.board[xrandom][yrandom] != "") {
          (xrandom = randomX()), (yrandom = randomX());
          console.log(xrandom, yrandom);
        }

        this.board[xrandom][yrandom] = this.player;
        this.player = this.player == "X" ? "O" : "X";
      }
      function randomX() {
          return Math.floor(Math.random() * 3);
        }
    },
  
    resetBoard() {
      this.board = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
      this.player = "X";
      this.count = 0;
    },
  },
};
</script>

<style scoped>
.area {
  margin: auto;
  height: 300px;
  width: 300px;
}

.row {
  display: flex;
}

.column {
  color: white;
  justify-content: center;
  display: flex;
  align-items: center;
  cursor: pointer;
  border: 2px solid white;
  height: 100px;
  background-color: rgb(78, 78, 233);
  width: 100px;
}
.column:hover {
  background-color: cornflowerblue;
}

button {
  border: 1px solid gainsboro;
  padding: 10px;
  width: 100px;
  margin: 10px;
}
</style>