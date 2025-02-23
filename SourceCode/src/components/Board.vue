

<template>
    <div class="container">
        <h1 v-if="winner" class="displayPlayer">Player {{ winner }} wins !</h1>
        <h1 v-else-if="draw">Game Draw</h1>
        <h1 v-else class="displayPlayer">Player {{ currentPlayer }}'s turn</h1>
        <div class="board">
            <Cell v-for="(cell, index) in board" :key="index" :value="cell" @Click="makeMove(index)"/>
        </div>
        <button @click="resetGame">Reset Game</button>
    </div>
</template>

<style scoped>
.board{
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    padding: 7px;
    background-color: cornflowerblue;
}

.container{
    display: flex
;
    justify-content: center;
    align-items: center;
    width: 500px;
    flex-wrap: wrap;
}

.displayPlayer{
    color: green;
    width: auto;
    flex-basis: 100%;
    text-align: center;
}
</style>


<script>
import Cell from './Cell.vue';

export default{
    data(){
    return {board: Array(9).fill(null),
        currentPlayer: "X",
        winner: null,
        draw: false
    }
},
components:{
    Cell
},
methods:{
    makeMove(cellIndex){
        if(!this.board[cellIndex] && !this.winner) //If the cell is empty
        {
            console.log("makeMove called");
            this.board[cellIndex] = this.currentPlayer;             //set cell value
            this.checkWinner();
            console.log("check draw: "+this.checkDraw());
            this.currentPlayer = this.currentPlayer=="X"?"O":"X";   // switch player
        }
    },
    checkWinner(){
        console.log("checkWinner called");
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
                this.winner=this.currentPlayer;
                console.log("winner: "+this.winner);
            }
        })

    },
    checkDraw(){
        // this.board.forEach((item, index)=>{
        //     if(item == null){
        //         this.draw= false;
        //         return this.draw;
        //     }
        //     else if(item!=null && index==this.board.length-1)
        //     {
        //         this.draw= true;
        //     }
        // });
        // return this.draw;
        //this.draw = this.board.find((item)=>item!=null);
        console.log("draw:" +this.draw);
        console.log("board:"+ this.board.length);
        return this.draw;
    },

    resetGame(){
        this.board.fill(null);
        this.winner = null;
        this.currentPlayer = "X";
    }
}
}
</script>