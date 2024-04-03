<script setup>

</script>

<template>
    <div class="right_column ">
        <img src="../img/Bubble 1.png" class="bubble1">
        <img src="../img/Bed.png" class="bed">
        <img src="../img/Bubble 4.png" class="bubble4">
    </div>
</template>

<style scoped>
    img{
        object-fit: contain;
        height: 100px;
    }

    .right_column{
        max-width: 420px;  
        width: 420px;
        min-width: 280px;
        height: 100%;
        display: flex;
        flex-direction: column;    
    }
    .bubble1{
        margin-top: 100px;
        margin-right: 100px;
        width: 160px;
    }
    .bed{
        width: 120px;
        margin-left: auto;
    
    }
    .bubble4{
        width: 220px;
        margin: auto;
    }
   
</style>
