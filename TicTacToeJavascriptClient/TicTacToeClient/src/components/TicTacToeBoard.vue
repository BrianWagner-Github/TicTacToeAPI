<script>
/* eslint-disable */
</script>
<template>
  <div class="TicTacToeBoard container">
    <div id="gamemenu" class="row text-center jumbotron mt-5" v-if="firstPlayer==null">
      <div class="col-12">
        <h1>Tic-Tac-Toe</h1>
        <button type="button" class="btn btn-primary btn-lg" v-on:click="startGame('O')">I Go First</button>
        <button type="button" class="btn btn-success btn-lg" v-on:click="startGame('X')">AI Goes First</button>
      </div>
    </div>
    <div id="gameboard" class="row mt-4" v-if="firstPlayer!=null">
      <div class="col-2">
        <button type="button" class="btn btn-danger" v-on:click="resetBoard()">Reset Game</button><br/>
        Winner: {{winner}}
      </div>
      <div class="col-10">
          <div class="row">
            <div class="col board-cell text-center" v-for="(item, index) in board.slice(0,3)" v-on:click="fillMove(index)">
              {{item}}
            </div>
          </div>
          <div class="row">
            <div  class="col board-cell text-center"   v-for="(item, index) in board.slice(3,6)" v-on:click="fillMove(index+3)">
              {{item}}
            </div>
          </div>
          <div class="row">
            <div  class="col board-cell text-center"  v-for="(item, index) in board.slice(6,9)" v-on:click="fillMove(index+6)">
              {{item}}
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TicTacToeBoard',
  mounted(){
  },
  data () {
    return {
      baseUrl: "https://localhost:44305//executeMove",
      winner: "inconclusive",
      firstPlayer: null,
      blankSymbol: '?',
      azurePlayerSymbol: 'X',
      userPlayerSymbol: 'O',
      board: ['?', '?', '?', '?', '?', '?', '?', '?', '?'],
      
    }
  },
  methods: {
    fillMove: function (index) {
      if(this.board[index] == this.blankSymbol ){
        this.board[index] = 'O';
         this.updateBoard();
      }
    },
    updateBoard: function (){
      if(this.winner == "inconclusive"){
          this.axios({
            method: 'post',
            url: this.baseUrl,
            data: {
              gameboard: this.board
            },
            withCredentials: false})
            .then(function (response) {
            this.board = response.data.gameBoard;
            this.winner = response.data.winner;
             this.$forceUpdate();
            }.bind(this));
           
      }
    },
    resetBoard: function(){
      this.board = ['?', '?', '?', '?', '?', '?', '?', '?', '?'];
      this.firstPlayer = null;
      this.winner = "inconclusive";
      this.$forceUpdate();
    },
    startGame: function(player){
      this.firstPlayer = player;
      if(this.firstPlayer == this.azurePlayerSymbol){
        this.updateBoard();
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board-cell{
  height: 30vh;
  border: 1px solid black;
  padding-top:5%;
  font-size:50px;
}
</style>
