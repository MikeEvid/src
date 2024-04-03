<script >

// const scrollRef = ref()
 export default {
    props: {
        game_finish_callback:{
            type: Function,
            required: true
        }
    },
    created() {
        window.addEventListener('scroll', this.moveProgress);
    },
    mounted() {
        this.$refs.gameArea2.scrollTo({
            top: 300,
            left: 0,
            behavior: "smooth",
        });
    },
    data (){
        return {
            mousePressRightNow: false,
            timerCount: 0,
            positionTop: 0,
            lastPosY : 0,
            lips_name_pic: 'src/img/coil/lips_closed_1 1.png',
            machine_handle_name_pic: 'src/img/coil/1@4x.png',
            machine_shfit: 'margin-bottom:100%; margin-top:-250%',
            time_last_touch: 0, // для отслеживания двойных нажатий / скролл-событий  на больших экранах
            // machine_handle_position:
            game_progress: 0,
            game_title_animation_timer: 0,
            game_progress_finish: 1000 // индекс - как долго идет игра
        }
    },
    watch: {
        timerCount: {
            handler() {
                    setTimeout(() => {
                        this.timerCount++;
                        this.tik();
                    }, 1000);
            },
            immediate: true 
        }
     },
    methods: {
        touchMove() { 
            this.moveProgress();
        },
        tik () {
            if(this.timerCount % 5 == 0) {// добавляем класс скрытия когда таймер кратен 5 секундам
                this.logoClass = 'zoom-leave-active';
                this.$refs.regLogo.classList.add('zoom-leave-active');
                this.$refs.regLogo.classList.remove('zoom-enter-active');

            } else if(this.timerCount % 5 == 1){ // убираем  класс когда таймер кратен 5 сек + 1
                this.$refs.regLogo.classList.add('zoom-enter-active');
                this.$refs.regLogo.classList.remove('zoom-leave-active');

            } 
            
            if(this.timerCount % 20 == 5){
                this.$refs.regHelper.classList.add('regHelper-Wave');
            } else if( this.timerCount % 20 == 9){
                this.$refs.regHelper.classList.remove('regHelper-Wave');
            }else if(this.timerCount % 20 == 14){
                this.$refs.regHelper2.classList.add('regHelper-Wave');
            }else if(this.timerCount % 20 == 19){
                this.$refs.regHelper2.classList.remove('regHelper-Wave');
            }

        },
        moveProgress (event) {
            if(this.time_last_touch != Math.round(Date.now()/1) && this.lastPosY < event.clientY){
    
                this.time_last_touch = Math.round(Date.now()/1);
                ++this.game_progress;     

                if(this.game_progress > this.game_progress_finish)
                    this.game_finish_callback();

                if(this.game_progress > 300)
                    this.lips_name_pic = 'src/img/coil/lips_opened 1.png';
                // движение языка через переменную pos
                let pos = Math.round((this.game_progress / 4) % 19);
                ++pos;
                if (pos > 10)
                    pos = 21 - pos;
                if (this.game_progress <  this.game_progress_finish) {
                    this.machine_handle_name_pic = "src/img/coil/" + pos +"@4x.png"
                    this.machine_shfit = "margin-bottom:"+ Math.round((1000 - this.game_progress)/10)+"%; margin-top:-"+ 2.5*Math.round((1000 - this.game_progress)/10)+"%; ";
                }
            }
            this.lastPosY = event.clientY;
        },
        touch (event){
            const touch = event.changedTouches[0];   
            this.moveProgress(touch);
            document.documentElement.scrollTop = 0;
        },
        mouse (event) {
            if(this.mousePressRightNow)
                this.moveProgress(event);
        },
        mouseStart2 () {
             this.mousePressRightNow = true;
        },
        mouseStop () {
            this.mousePressRightNow = false;

        }
    }
}
</script>

<template>
    <div class="game_column column noselect2 onlyMobileMargin" 

        ref="gameArea">
        <img src="../img/logo.png" class="logo"  ref="regLogo">
            <img :src="lips_name_pic" class="lips">
        <div class="img_row">
            <img src="../img/coil/machine_1@4x.png" class="machine">
            <img :src="machine_handle_name_pic" class="handle">
        </div>
        <div class="tongue_area"   ref="scrollRef">
            <img src="../img/coil/1.png" :style="machine_shfit"/>

            <div class="empty"> </div>

        </div>
        <img src="../img/helper1.png" class="regHelper" ref="regHelper"/>
        <img src="../img/helper2.png" class="regHelper2" ref="regHelper2"/>
        <span class="touchArea"
            id="gameArea2"
            ref="gameArea2"
            @mousedown="mouseStart2"
            @mouseup="mouseStop"
            @mouseleave="mouseStop"
            @mousemove="mouse"
            @touchstart="touch"
            @touchmove="touch"
        > 
            <div v-for="index in 1000" :key="index">
                <br/>  
            </div>
    </span>
    </div>
</template>

<style scoped>
    .touchArea{
        background-color: lightgreen;
        opacity: 0;
        position: absolute;
        width: 100%;
        height: 100%;
        overflow-y: scroll;
        cursor: pointer;
    }
    .regHelper,
    .regHelper2{
        position: absolute;
        height: 80px;
        bottom: 20px;
        opacity: 0;
    }
    .regHelper2{
        /* right:0; */
        margin-left: 180px;
        bottom: 100px;
    }
    .empty{
        min-height: 900px;
    }
    .lips{
        width: 220px !important;
        margin-top: 40px;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: -20px;
    }
    .tongue_area div{
        display: flex;
    }
    .tongue_area{
        
        height:  calc(100% - 10px);
        /* background-color: lightpink; */
        /* overflow-y: scroll; */
        overflow: hidden;
        display: flex;
        /* flex-direction: column-reverse; */
        margin-top: -80px;
        scrollbar-width: 0px
    }
    .tongue_area::-webkit-scrollbar {
        display: none;
    }

    .tongue_area img{
        margin-top: -4px;;
        margin-left: auto;
        margin-right: auto;
        width: 150px;
        object-fit: contain;
    }
    .img_row{
        margin-top: -40px;
        display:  flex;
        flex-direction: row;
        position: relative;
    }
    .handle{
        position: absolute;
        right: 0px;
        width: 84px;
    }
    .logo{
        margin: 20px auto;
        height: 36px;
    }
    .machine{
        margin: 20px auto;
        width: 200px !important;
    }
    .game_column{
        background-image: url("../img/Rectangle 5.png");
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
        max-height: 90%;
        margin: auto 0px; 
        overflow: hidden;
        /* position: relative; */
    }

    .zoom-enter-active {animation: zoom-in 1s ease-in-out;}
    .zoom-leave-active {animation: zoom-out 1s ease-in-out;}
    @keyframes zoom-in {
        from {transform: scale(0.5,0.5);
           ;}
        to {transform: scale(1,1);}
    }
    @keyframes zoom-out {
        from {transform: scale(1,1);}
        to {transform: scale(0.5,0.5);}
    }

    .regHelper-Wave {animation: helperWave 4s ease-in-out;}
    /* .regHelper-down {animation: helperDown 1s ease-in-out;} */
    @keyframes helperWave {
        0% {
            display: none;
            opacity: 0;
            margin-bottom: 300px;
 
        }
        30% {
            display: block;
            opacity: 1;
            margin-bottom: 50px;
        }
        80% {
            display: block;
            opacity: 1;
            margin-bottom: 50px;
        }
        100% {
            display: block;
            opacity: 0;
            margin-bottom: 0px;
        }
    }

</style>
