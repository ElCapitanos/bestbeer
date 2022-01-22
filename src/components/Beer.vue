<template>
  <section>
    <div class="beer-card">
      <img class="beer-card__pict" src="pict/beer.jpg" :alt="beerArr.name" />
      <div class="beer-card__info">
        <div class="beer-card__name beer-card__stroke">
          NAME: {{ beerArr.name }}
        </div>
        <div class="beer-card__style beer-card__stroke">
          STYLE: {{ beerArr.style }}
        </div>
        <div class="beer-card__brand beer-card__stroke">
          BRAND: {{ beerArr.brand }}
        </div>
        <div class="beer-card__alcohol beer-card__stroke">
          ALCOHOL: {{ beerArr.alcohol }}
        </div>
        <div class="beer-card__blg beer-card__stroke">
          BLG: {{ beerArr.blg }}
        </div>
        <div class="beer-card__hop beer-card__stroke">
          HOP: {{ beerArr.hop }}
        </div>
        <div class="beer-card__ibu beer-card__stroke">
          IBU: {{ beerArr.ibu }}
        </div>
        <div class="beer-card__malts beer-card__stroke">
          MALTS: {{ beerArr.malts }}
        </div>
      </div>
    </div>
    <div class="button-block">
      <button class="button-beer" @click="showOverlay(), showBender()">
        right!
      </button>
      <button class="button-beer" @click="getBeer(), getAnswer()">
        are you nuts?!
      </button>
    </div>
    <button
      class="button-beer button-beer__secret"
      @click="showOverlayQuestion(), showQuestion()"
    >
      secret button
    </button>
    <div class="overlay" @click="finishIt()"></div>
    <div class="overlay overlay__question"></div>
    <div class="question">
      <span class="question__text">want a decent beer?</span>
      <div class="button__block button__block_popup">
        <button class="button__popup" @click="letsContinue()">No!</button
        ><button class="button__popup" @click="showOverlay(), closeOverlayQuestion(), letsBeer()">Yes...</button>
      </div>
    </div>
    <div class="finish">
      <img src="pict/homebender.png" alt="Hooray!" class="finish__pict" />
      <span class="cross" @click="finishIt()">&times;</span>
    </div>
    <div class="finish__well">
      <img src="pict/best.jpg" alt="Hooray!" class="finish__pict" />
      <span class="cross" @click="finishIt()">&times;</span>
    </div>
  </section>
</template>
<script>
export default {
  name: "User",
  data() {
    return {
      beerArr: [],
    };
  },
  methods: {
    getBeer() {
      fetch("https://random-data-api.com/api/beer/random_beer")
        .then((res) => res.json())
        .then((data) => {
          this.beerArr = data;
        });
    },
    getAnswer() {
      document.querySelector(".button-beer__secret").style.display = "block";
    },
    showOverlay() {
      document.querySelector(".overlay").style.display = "block";
    },
    showOverlayQuestion() {
      document.querySelector(".overlay__question").style.display = "block";
    },
    closeOverlayQuestion() {
      document.querySelector(".overlay__question").style.display = "none";
    },
    finishIt() {
      window.location.reload();
    },
    showBender() {
      document.querySelector(".finish").style.display = "block";
    },
    showQuestion() {
      document.querySelector(".question").style.display = "flex";
    },
    letsContinue() {
        document.querySelector(".question").style.display = "none";
        document.querySelector(".overlay__question").style.display = "none";
    },
    letsBeer() {
        document.querySelector(".finish__well").style.display = "block";
        document.querySelector(".question").style.display = "none";
    }
  },
  mounted() {
    this.getBeer();
  },
};
</script>
<style lang="sass" scoped>
.finish__well
    display: none
    position: absolute
    top: 20px
    left: 50%
    transform: translateX(-50%)
    max-height: 80%
    background-color: #fff
    z-index: 30
    padding: 10px
    box-sizing: border-box
    border-radius: 10px
.question
    padding: 0 20px
    box-sizing: border-box
    display: none
    flex-direction: column
    width: 310px
    height: 200px
    background-color: #fff
    position: absolute
    top: 50%
    left: 50%
    transform: translate(-50%, -50%)
    border-radius: 8px
    z-index: 25
.overlay__question
    z-index: 22
.question__text
    display: block
    margin: 40px 0
    text-transform: uppercase
    font-weight: 200
    user-select: none
.button__popup
    font-size: 16px
    line-height: 30px
    width: 46%
    background-color: #ebebeb
    text-transform: uppercase
    cursor: pointer
    transition: .4s linear
    border-radius: 4px
    &:hover
        background-color: #000
        color: #fff
.button__block_popup
    display: flex
    justify-content: space-around
.finish
    display: none
    width: 70%
    position: absolute
    top: 20px
    left: 50%
    transform: translateX(-50%)
    background-color: #fff
    z-index: 30
    padding: 10px
    box-sizing: border-box
    border-radius: 10px
.finish__pict
    width: 100%
.cross
    font-size: 30px
    font-weight: 700
    position: absolute
    top: 15px
    right: 15px
    color: #000
    background-color: #fff
    width: 40px
    height: 40px
    border: solid 5px #000
    border-radius: 50%
    box-sizing: border-box
    cursor: pointer
    line-height: 32px
.overlay
    display: none
    position: fixed
    top: 0
    left: 0
    z-index: 20
    width: 100%
    height: 100%
    background-color: rgba(0,0,0, .7)
.beer-card
    display: flex
    flex-direction: row
    padding: 5px
    border: solid 1px grey
    box-sizing: border-box
    border-radius: 6px
    box-shadow: 1px 1px 20px rgba(0,0,0, .5)
    background-color: #fff
    max-width: 700px
    margin: 20px auto
.beer-card__pict
    width: 300px
    height: 300px
    display: block
    margin-right: 20px
    @media screen and (max-width: 680px)
      width: 200px
      height: 200px
    @media screen and (max-width: 420px)
      width: 180px
      height: 180px
.beer-card__info
    margin-top: 10px
    display: flex
    flex-direction: column
    text-align: left
    @media screen and (max-width: 680px)
      font-size: 12px
    @media screen and (max-width: 420px)
      font-size: 10px
.beer-card__stroke
    line-height: 2
    font-weight: 300
.button-beer
    width: 48%
    padding: 10px 0
    text-transform: uppercase
    font-weight: 700
    cursor: pointer
    transition: .4s linear
    background-color: #fff
    color: #000
    border: solid 1px grey
    border-radius: 2px
    box-sizing: border-box
    &:hover
        background-color: #000
        color: #fff
            border: solid 1px #000
.button-block
    width: 100%
    max-width: 700px
    margin: 10px auto
    display: flex
    justify-content: space-between !important
.button-beer__secret
    width: 100%
    max-width: 700px
    margin: 10px auto
    display: none
</style>
