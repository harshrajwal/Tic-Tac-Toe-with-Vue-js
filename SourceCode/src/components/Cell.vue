<template>
    <div>
        <button class="cell" v-bind:class="{winnerCell: winnerIndex}">{{ value }}</button>
    </div>
</template>

<style scoped>
.cell{
    background-color: azure;
    height: 100px;
    width: 100px;
    padding: 2px;
    font-size: 3rem;
    color: darkorchid;
}

.winnerCell{
    background-color: greenyellow;
}
</style>

<script>
export default{
props: ['value', 'winnerIndex']
}

</script>