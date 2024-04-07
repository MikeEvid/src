<script setup>

</script>

<template>
 <!-- // отображение элементо дизайна главной старницы -->
 <div class="fullSpace2" className="fullSpace2">


  <img src="../img/Ellipse 2.png" class="ellipse2">
  <img src="../img/Ellipse 34.png" class="ellipse34">
  <img src="../img/Ellipse 37.png" class="ellipse37">
  <img src="../img/Ellipse 49.png" class="ellipse49">
  <img src="../img/Ellipse 50.png" class="ellipse50">
  <!-- <div class="backgroundForMobile"></div> -->
 </div>
</template>

<style scoped>
/* 
  .backgroundForMobile{
    position: fixed;
    width: 100vw;
    height: 100vh;
  } */
  .fullSpace2{
    position: absolute;
    height: 100vh;
    width: 100vw;
    min-width: 600px;
    overflow: hidden;
     /* min-width: none; */

    /* display:  */
  }


  @media  (max-width: 868px) {
    img{
      display: none;;
    }
    .fullSpace2{
      /* background-color: #56B1BC; */
      background-image: url("../img/Rectangle 5.png");
      background-repeat: no-repeat;
      background-size: cover;
    }
  }
  .fullSpace2 img{
    position: absolute;

  }
  .ellipse2{
    top: 100px ;
    right: 0px;
  }
  .ellipse34{
    left: 0;
    top: 0;
  }
  .ellipse37{
    right: 0;
    bottom: 100px;
  }
  .ellipse50{
    left: 140px;
    bottom: 0px;
  }
  .ellipse49{
    width: 520px;
    height: 520px;;
    left: calc(50% - 260px);
    top:  calc(50% - 260px);
  }
</style>
