<script >
    export default {
        props:{
            startGame: {
                type: Function,
                required: true
            }
        }
    }

</script>

<template>
    <div class="center_column onlyMobileMargin">
        <!-- <BackgroundElements/> -->
        <!-- <img src="../img/Стартовый.png"/> -->
        <img src="../img/Logo.png" class="logo"/>
        <div class="border_primary_color">
            <img src="../img/mainPic.jpg"/>
        </div>
        <button v-on:click="startGame">Раскатать губу</button>
    </div>
</template>

<style scoped>
    button{
        background-color: #D33737;
        color: white;
        border-radius: 12px;
        border: 0px;
        height: 52px;
        width: 300px;
        margin: auto;
        font-size: large;
        margin-top: 40px;
    }
    .logo{
        object-fit: contain;
        height: 30px;
        margin: 20px auto;

    }
    h1{
        text-align: center;
        color: #FAE07B;
    }
    .border_primary_color{
        border: 2px solid #FAE07B;
        width: 300px;
        /* height: 300px; */
        margin: auto;
        border-radius: 16px;
        overflow: hidden;
    }


    .border_primary_color img{
        width: 100%;
    }
    .center_column{
        border: 10px solid #2E6C77;
        border-radius: 20px;
        max-width: 360px;  
        min-width: 360px;
        width: 360px;
        padding: 20px;
        height: 100%;
        display: flex;
        flex-direction: column;   
        margin: auto 0px; 
    }
    button:hover{
        background-color: red;
        cursor: pointer;
    }
   
</style>
