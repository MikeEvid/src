<script >
  import BackgroundElements from './components/BackgroundElements.vue'
  import Footer from './components/Footer.vue'
  import LeftColumn from './components/LeftColumn.vue'
  import RightColumn from './components/RightColumn.vue'
  import CenterColumn from './components/CenterColumn.vue'
  import GameArea from './components/GameArea.vue'
  import PromoArea from './components/PromoArea.vue'
  import axios from "axios"


  export default {
    components: {BackgroundElements, Footer, LeftColumn, RightColumn, CenterColumn, GameArea, PromoArea},
    data (){
      return {
        state_page: 0,
        local_udid: '',
        utm_source: '',
        utm_campaign: '',
        promo : '',
      }
    },
    created() {
      this.readParams();
    },
    methods: {
      readParams () {
        // чтение параметров из запроса
        let urlParams = new URLSearchParams(window.location.search);
        this.utm_campaign = urlParams.has('utm_campaign') ? urlParams.get('utm_campaign') : '-';
        this.utm_source = urlParams.has('utm_source') ? urlParams.get('utm_source') : '-';

        if (!localStorage.getItem("udid")) {
          this.local_udid = 'a' + Math.random().toString(36).slice(2,11);
          localStorage.setItem('udid', this.local_udid);
        } else {
          this.local_udid = localStorage.getItem('udid');
        }

        axios.get("https://festapp.ru/api/v1_abc/askona/udid/"+ this.local_udid)
          .then(response => {
            if(response.data.status == 200){
              console.log(response.data);
              if(response.data.status == 200 && parseInt(response.data.data) > 1){
                this.promo = response.data.data;
               // this.state_page = 2;
              }
            }
          });
      },
      play_game() {
        this.state_page = 1;
        // this.game_finish_callback();
      },
      async game_finish_callback() {

        let dataToServ = { utm_source: this.utm_source,
                          utm_campaign: this.utm_campaign};

        if (this.state_page == 1)
          axios.post("https://festapp.ru/api/v1_abc/askona/udid/"+ this.local_udid, JSON.stringify(dataToServ))
            .then(response => {
              if(response.data.status == 200){
                this.promo = response.data.data;
                this.state_page = 2;
              }
            });   

          this.state_page = 2;
      }
    }

 }

</script>

<template>
  <div class="main_container " >
    <BackgroundElements className="fullSpace2 "/>
    <div  class="row_main_columns onlyMobileMargin ">
      <LeftColumn class="notMobile  "/>
      <CenterColumn v-if="state_page==0" :startGame="play_game" class="onlyMobile mobileZoom " />
      <GameArea v-else-if="state_page==1" :game_finish_callback="game_finish_callback" class="onlyMobile mobileZoom"/>
      <PromoArea v-else-if="state_page==2" :promo="promo" class="onlyMobile mobileZoom"/>
      <RightColumn  class="notTablet "/>
    </div>
    <Footer class="notMobile"/>
  </div>

</template>

<style scoped>


.fullSpace2{
    position: absolute;
    height: 100vh;
    width: 100vw;
  }
  .fullSpace2 img{
    position: absolute;
  }

  @media  (max-width: 1160px) {
    .notTablet {
      display: none;
    }
  }

  @media  (max-width: 868px) {
    .main_container{
      justify-content: end;
    }
    .row_main_columns{
      margin-top: 20px !important;
    }
    .mobileZoom{
      /* transform: scale(1.2); */
    }
    .notMobile {
        display: none;
    }
    .onlyMobile{     
      width: 100% !important;
      max-height: 100% !important;
    }
    .onlyMobileMargin{
      /* background-color: red !important; */
      border: none !important
    }
  }

  .main_container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    max-height: 100% !important;
    /* background-color: red;; */
  }
  .row_main_columns{
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    min-height: 740px;
    max-height: 940px;;
    max-width: 1600px;
    min-width: 400px;
    width: 100%;
    margin: auto;
  }
  .borderW{
    border:3px solid  lightcyan;
  }
</style>
