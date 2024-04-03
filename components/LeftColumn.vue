<script setup>

</script>

<template>
    <div class="left_column">
        <img src="../img/Logo.png" class="logo"/>
        <h1 class="mtb">Как играть</h1>
        <ul class="mtb">
            <li><span>Скролльте экран вниз, чтобы губа растягивалась.</span></li>
            <li><span>Получайте промокод, выигрывайте 50 000 рублей!</span></li>
            <li><span>Попадите в «Рейтинг дерзости» и увеличьте шансы на победу!</span></li>
        </ul>
        <div class="mtb row_imgs">
            <img src="../img/Bubble 3.png">
            <img src="../img/sofa.png">
        </div>
    </div>
</template>

<style scoped>
    .mtb{
        margin-top: auto;
        margin-bottom: auto;
    }
    .left_column{
        padding: 40px 20px;
        max-width: 360px;  
        width: 360px;
        height: 100%;
        display: flex;
        flex-direction: column;    

        font-family: "Gilroy-Light";
    }
    .logo{
        margin-bottom: 100px;
        width: 200px;
        margin-left: auto;
        margin-right: auto;
    }
    .row_imgs{
        /* margin: 10px auto 10px;
         */
        display: flex;
        flex-direction: row;
        justify-content: space-around
    }
    h1{
        color: #FAE07B;
        width: 100%;
        text-align: center;
        font-family: "Gilroy-ExtraBold";
    }
    li {
        color: #FAE07B;
        font-size: large;
        margin-bottom: 30px;
    }
    span {
        color: white;;
    }
  
</style>
