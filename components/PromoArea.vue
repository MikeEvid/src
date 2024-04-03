<script >
 export default {
    props: {
        promo:{
            type: String,
            required: true
        }
    },
    data (){

    },
    methods: {
        preparedPromo () {
            let promo_number = 10000 + parseInt(this.promo);
            return 'PROMO' + promo_number.toString().substring(1,5);
        },
        async copyInClipboard () {
            try {
                await navigator.clipboard.writeText(this.preparedPromo())
                console.log('Text copied to clipboard successfully!')
            } catch (error) {
                console.error('Failed to copy text:', error)
            }
        }
    }
}
</script>

<template>
    <div class="promo_column column onlyMobileMargin">
        <img src="../img/logo.png" class="logo">
        <div class="bottom_area column">
            <b class="title">Кровать Elisa</b>
            <img src="../img/krovat.png" class="krovat"/>
            <b>Ваша дополнительная скидка:</b>
            <span>5% на покупку в рассрочку</span>
            <div class="promo_area">
                <b>{{ preparedPromo() }}</b>
                <button @click="copyInClipboard">
                    <img src="../img/Copy.png"/>
                </button>
            </div>
            <b>Оформите рассрочку до 31.05<br/>и выиграйте 1 000 000 рублей!</b>


        </div>
     
    </div>
</template>

<style scoped>
    .krovat{
        object-fit: contain;
        width: 122px;
        margin: 20px auto;
    }
    .promo_area{
        background-color: #FAE07B;
        border-radius: 12px;
        padding: 6px;
        height: 29px;
        width: 148px;
        margin: 20px auto;
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        
    }
    .promo_area button{
        background-color: #FAE07B;
        outline: none;
        border: 0px;
        /* animation-duration: 500ms; */
    }
    .promo_area b{
        /* background-color: aqua; */
        /* margin-top: -10px; */
    }

    .promo_area button:hover
    {
        transform: scale(1.1);
    }
    .title{
        font-size: x-large;
    }
    .bottom_area{
     background-color: white;  
     width: 300px;
     height: 360px; 
     margin: auto;
     margin-bottom: 0px;
     padding: 20px;
     border-radius: 20px 20px 00px 0px;
     text-align: center;
     line-height: 30px;
        font-family: "Gilroy-Light";
     /* font-size: 14px; */
    }
    b{

        /* font-family: ""; */
    }
   
    .promo_column{
        background-image: url("../img/Rectangle 104.png");
        background-repeat: no-repeat;
        background-size: cover;
        /* background-color: red; */
        border: 10px solid #2E6C77;
        border-radius: 20px;
        max-width: 360px;  
        min-width: 360px;
        width: 360px;
        padding: 20px;
        padding-bottom: 0px;
        height: 100%;   
        margin: auto 0px; 
    }
    .logo{
        margin: 20px auto;
        height: 36px;
    }
</style>
