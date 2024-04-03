<script setup>

</script>

<template>
    <div class="footer">
      <div class="col">
        © 1990–2024. Компания «Кокоона»<br/>  
         Почта для обратной связи: igra@ kokona.ru
      </div>
     
      <div class="col">
        Подробные условия розыгрыша
        <br/>
        Подробнее о рассрочке
      </div>
    </div>
</template>

<style scoped>

  .footer{

    font-family: "Gilroy-Light";
    margin-top: 60px !important;
    margin: auto;
    padding: 4px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;

    max-width: 600px;
    position: relative;
    font-size: 14px;
    color: white;
  }
  .footer .col:first{
     margin: auto;
     margin-right: 20px;
  }
  .footer .col:last-child{
    margin-left: 20px;
    margin-right: auto;
  }
</style>
