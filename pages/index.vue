<template>
  <div class="body">
      <div :class="loading">
        <div class="bg-pattern first"></div>
        <div class="intro-sentence"> Cela nous concerne aussi... </div>
      </div>
      <GridBackground class="background" :columns="'0.4fr repeat(6, 1fr) 0.6fr'" :rows="'repeat(4, 1fr)'"> </GridBackground>
      <div class="content">
        <div class="navleft">
          <a class="points" href="#Intro1"> </a>
          <a class="points" href="#1CCTitre"> </a>
          <a class="points" href="#2RCTitre"> </a>
        </div>
        <div class="navright">
          <div class="logo">
            <img class="earth" @click="openCredit()" src="ressources/icon/red_round.svg">
          </div>
        </div>
        <full-page ref="fullpage" :options="options" id="fullpage">
          <div class="section">
           <Intro> </Intro>
          </div>
          <div class="section">
            <IntroPageTwo> </IntroPageTwo>
          </div>
          <div class="section">
            <IntroPageThree> </IntroPageThree>
          </div>
          <div class="section">
            <RCfirst
               title="Catastrophes climatiques"
               paragraph="Par catastrophes climatiques nous entendons toutes les catastrophes liées au climat.  Nous excluons ici les catastrophes naturelles à savoir : séismes, éruption volcaniques, ouragans."
               page="01"
               imageSrc="/ressources/img/image1.jpg"
               imageXPosition="1/4"
               imageYPosition="4/7"
            > </RCfirst>
          </div>
          <div class="section">
            <GraphDisplayPageOne
              title="Un constat surprenant"
              subTitle='Évolution dans le temps du nombre de catastrophes climatiques à l’échelle mondiale '
              page="01">
            </GraphDisplayPageOne>
          </div>
          <div class="section">
            <GraphDisplayPageTwo
              title="Qu’en est-il en France ?"
              subTitle='Nombre d’évènements et de victimes par aléa en France en 2019'
              page="01">
            </GraphDisplayPageTwo>
          </div>
          <div class="section">
            <GraphDisplayPageThree
              title="Zoom sur la canicule "
              subTitle='Population exposée à au moins une canicule dans l’été en France en millions d’habitants.'
              page="01">
            </GraphDisplayPageThree>
          </div>
          <div class="section">
            <VariousStatsPageFour>

            </VariousStatsPageFour>
          </div>
          <div class="section">
            <SecondTitle
              title="Catastrophes climatiques"
              paragraph="Depuis le début du XXème siècle on observe une hausse des températures moyennes atmosphériques et océaniques du fait d’émissions de gaz à effet de serre excessives."
              page="02"
              imageSrc="/ressources/img/image11.jpg"
              imageXPosition="1/5"
              imageYPosition="2/5"
            > </SecondTitle>
          </div>
          <div class="section">
            <GraphDisplayPageFive
              title="Coïncidence ou corrélation ?"
              subTitle='Ecarts des températures en C°  et évolution du nombre de catastrophes climatique sur la période 1950 et 2018'
              page="02"
              > </GraphDisplayPageFive>
          </div>
          <div class="section">
            <GraphDisplayPageSix
              title="L’être humain dans tout ça ?"
              subTitle='Répartition des émissions de CO2 par secteurs en France en 2017 (en millions de tonnes de CO2)'
              page="02"
            > </GraphDisplayPageSix>
          </div>
          <div class="section">
            <Conclusion>

            </Conclusion>
          </div>
        </full-page>
      </div>
      <Credit
        @close="openCredit()"
        :class="CreditOpen"
      >
      </Credit>
  </div>
</template>

<script>
  import Vue from 'vue'
  import VueFullPage from 'vue-fullpage'

  Vue.use(VueFullPage);

  import GridBackground from "../components/GridBackground.vue";
  import GraphDisplay from "../components/GraphDisplayPageOne.vue";
  import RCfirst from "../components/RCFirst.vue";
  import Credit from "../components/Credit.vue";
  import Intro from "../components/Intro.vue";
  import GraphDisplayPageOne from "../components/GraphDisplayPageOne";
  import GraphDisplayPageTwo from "../components/GraphDisplayPageTwo";
  import GraphDisplayPageThree from "../components/GraphDisplayPageThree";
  import VariousStatsPageFour from "../components/VariousStatsPageFour";
  import GraphDisplayPageFive from "../components/GraphDisplayPageFive";
  import GraphDisplayPageSix from "../components/GraphDisplayPageSix";
  import Conclusion from "../components/Conclusion";
  import IntroPageTwo from "../components/IntroPageTwo";
  import IntroPageThree from "../components/IntroPageThree";
  import RCFirst from "../components/RCFirst";


  export default {
    components: {
      GraphDisplay,
      RCfirst,
      Intro,
      GraphDisplayPageOne,
      GraphDisplayPageTwo,
      GraphDisplayPageThree,
      VariousStatsPageFour,
      GraphDisplayPageFive,
      GraphDisplayPageSix,
      Conclusion,
      IntroPageTwo,
      IntroPageThree,
      Credit,
      GridBackground,
      VueFullPage
    },
    data() {
      return {
        loading: 'loading',
        CreditOpen: 'Credit isNotOpen',
        options: {
          licenseKey: '2771A04F-45AB4BE7-9E833A0A-2325C142',
          menu: '#menu',
          anchors: ['Intro1', 'Intro2', 'Intro3', '1CCTitre', '1CCPage1', '1CCPage2', '1CCPage3', '1CCConclu', '2RCTitre', '2RCPage1', '2RCPage2', 'Conclu']
        },
        page: "01",
        animateCredit: false,
      }
    },
    async mounted() {
      await this.waitforloading();
      document.addEventListener('DOMContentLoaded',() => {
          this.test('test the loading')
      });
    },
    methods: {
      test(test){
        console.log('test', test)
      },
      waitforloading() {
        setTimeout(() => {
          this.loading = 'loading stop'
        }, 2000)
      },
      openCredit() {
        if (this.CreditOpen == 'Credit isNotOpen') {
          this.CreditOpen = 'Credit isOpen'
        } else if (this.CreditOpen = 'Credit isOpen') {
          this.CreditOpen = 'Credit isNotOpen'
        }
      }
    },
  }

</script>

<style lang="scss">
  .body {
    position: fixed;
    margin-left: 0;
    width: 100%;
    height: 100vh;

    .Credit {
      position: absolute;
      z-index: 7;
      width: 100%;
      height: 100vh;
      left:0;
      transition-duration: 0.7s;

      &.isOpen {
        top: 0;
      }

      &.isNotOpen {
        top: -100vh;
      }
    }

    .loading {
      position: absolute;
      z-index: 10;
      width: 100%;
      height:100vh;
      top:0;
      left:0;
      background-color: white;
      display: grid;
      grid-template-columns: 0.4fr repeat(6, 1fr) 0.6fr;
      grid-template-rows: repeat(4, 1fr);
      overflow: hidden;

      .bg-pattern {
        background-image: url("/ressources/img/svg/motif.svg");
        background-size: cover;
        opacity: 0.07;

        &.first {
          grid-row: 1 / 5;
          grid-column: 1 / 9;
        }
      }
      .intro-sentence {
        font-size: 10vh;
        max-width: 80vw;
        margin: 40vh 10vw;
        font-family: Montserrat;
        text-align: center;
        position: absolute;
      }
    }

    .stop {
      transition-duration: 0.7s;
      top: -100vh;
    }

    .content {

      .logo {
        width: calc(100% / 7 * 0.6);
        position: absolute;
        right: 0;
        top: 0;
        z-index: 6;
        text-align: center;

        .earth {
          margin-top: 30px;
          width: 50px;
          height: 50px;
          cursor: pointer;
          //animation-name: anim_round;
          animation-duration: 5s;
          animation-iteration-count: infinite;
          animation-timing-function: linear;

          @keyframes anim_round {
            0% {
              transform: skew(5deg, -5deg);
            }
            25% {
              transform: skew(5deg, 5deg);
            }
            50% {
              transform: skew(5deg, -5deg);
            }
            75% {
              transform: skew(5deg, -15deg);
            }
            100% {
              transform: skew(5deg, -5deg);
            }
          }
        }
      }

      .navleft{
        position: absolute;
        z-index: 6;
        width: calc(100% / 7 * 0.4);
        height: 100vh;
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(4, 1fr);
        grid-column-gap: 0px;
        grid-row-gap: 0px;

        .points {
          position: absolute;
          transform: translateY(-50%) translateX(+50%);
          width: 13px;
          height: 13px;
          font-size: 0;
          border-radius: 100%;
          background-color: #D3D3D3;
          border: 0;
          cursor: pointer;
          right: 0;

          &:nth-of-type(1) {
            grid-row: 2;
          }

          &:nth-of-type(2) {
            grid-row: 3;
          }

          &:nth-of-type(3) {
            grid-row: 4;
          }
        }
      }

      #fullpage{
        width: 100vw;

        .fp-tableCell{
          vertical-align: unset;
        }
      }

    }

    #fullpage {
      z-index: 5;
    }

    .background {
      position: fixed;
      width: 100%;
      height: 100vh;
      z-index: 0;
    }
  }
</style>
