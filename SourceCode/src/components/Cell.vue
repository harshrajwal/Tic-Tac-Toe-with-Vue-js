<template>
    <div>
        <button class="cell">{{ value }}</button>
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
</style>

<script>
export default{
props: ['value']
// emits: ['cellClick'],
// methods:{
//     handleClick(){
//         this.$emit('cellClick');
//     }
// }
}

</script>