

<template>
    <div class="container">
        <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="125" height="125" />
        <h1>Tic-Tac-Toe</h1>
        <h1 v-if="winner" class="winner">Player {{ winner }} wins !</h1>
        <h1 v-else-if="draw">Game Draw</h1>
        <h1 v-else class="displayPlayer">Player {{ currentPlayer }}'s turn</h1>
        <div class="board">
            <Cell v-for="(cell, index) in board" :key="index"  :value="cell" 
            :winnerIndex="winningCell.includes(index)" @Click="playMove(index)"/>
        </div>
        <button class="btnReset" @click="resetGame">Restart Game</button>
    </div>
</template>

<style scoped>

/* For game board */
.board{
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    padding: 7px;
    background-color: cornflowerblue;
}

.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 500px;
    flex-wrap: wrap;
    gap: 10px;
}

/* For Current Player's turn */
.displayPlayer{
    width: auto;
    flex-basis: 100%;
    text-align: center;
}

/* For declared winner */
.winner{
    color: green;
}

/* For Reset button */
.btnReset{
    background-color: crimson;
    color: cornsilk;
    padding: 10px;
    font-size: larger;
    border-radius: 10px;
}
</style>


<script>
import Cell from './Cell.vue';      //using cell as component

export default{
    data(){
    return {board: Array(9).fill(null),
        currentPlayer: "X",
        winner: null,
        draw: false,
        winningCell: []
    }
},
components:{
    Cell
},
methods:{

    //Method when a player makes a move
    playMove(cellIndex){
        if(!this.board[cellIndex] && !this.winner) //case when the selected cell is empty
        {
            console.log("playMove called");
            this.board[cellIndex] = this.currentPlayer;             //set cell value
            this.checkWinner();                                     //check currentplayer is winner or not
            this.checkDraw();                                       // check game is draw or not
            this.currentPlayer = this.currentPlayer=="X"?"O":"X";   // switch player's turn
        }
    },

    //Method to check if the current player is winner or not
    checkWinner(){
        console.log("checkWinner called");

        //All possibilites of win
        const winPattern = [
            [0,1,2],[3,4,5],[6,7,8],
            [0,3,6],[1,4,7],[2,5,8],
            [0,4,8],[2,4,6]
        ];
        
        winPattern.forEach((pattern)=>{
            const[cellIndex1, cellIndex2, cellIndex3] = pattern;

            if(this.board[cellIndex1] && this.board[cellIndex1]==this.board[cellIndex2]
                && this.board[cellIndex2]==this.board[cellIndex3]
            ){
                this.winningCell = pattern;
                this.winner=this.currentPlayer;
                console.log("winner: "+this.winner);
            }
        })

    },

    //Method to check if the game is draw or not
    checkDraw(){
        this.draw = this.board.every((cell)=> cell!=null) && !this.winner;
    },

    //Method to restart the game when restart button is clicked
    resetGame(){
        this.board.fill(null);
        this.winner = null;
        this.currentPlayer = "X";
        this.draw = false;
        this.winningCell = [];
    }
}
}
</script>