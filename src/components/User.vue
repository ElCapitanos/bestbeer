<template>
  <section>
    <div class="user-card">
      <div class="user-card__pict-container">
        <img
          class="user-card__pict"
          v-if="isLoaded"
          @load="onImgLoad"
          :src="userArr.avatar"
          :alt="userArr.name"
        />
        <img
          class="user-card__pict"
          v-else
          src="pict/user.jpeg"
          :alt="userArr.name"
        />
      </div>
      <div class="user-card__info">
        <div
          v-if="
            userArr.first_name != undefined || userArr.last_name != undefined
          "
          class="user-card__name user-card__stroke"
        >
          NAME: {{ userArr.first_name }} {{ userArr.last_name }}
        </div>
        <div
          v-if="userArr.date_of_birth != undefined"
          class="user-card__birthday user-card__stroke"
        >
          BIRTHDAY: {{ userArr.date_of_birth }}
        </div>
        <div
          v-if="userArr.email != undefined"
          class="user-card__email user-card__stroke"
        >
          EMAIL: {{ userArr.email }}
        </div>
        <div
          v-if="userArr.phone_number != undefined"
          class="user-card__phone user-card__stroke"
        >
          PHONE: {{ userArr.phone_number }}
        </div>
        <div
          v-if="userArr.address != undefined"
          class="user-card__country user-card__stroke"
        >
          COUNTRY:
          {{ userArr.address.country }}
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "User",
  data() {
    return {
      userArr: [],
      isLoaded: false,
    };
  },
  methods: {
    getUser() {
      fetch("https://random-data-api.com/api/users/random_user")
        .then((res) => res.json())
        .then((data) => {
          this.userArr = data;
          console.log(this.userArr);
        });
    },
    randomColor() {
      let r = Math.floor(Math.random() * 256);
      let g = Math.floor(Math.random() * 256);
      let b = Math.floor(Math.random() * 256);
      let newColor = "rgba(" + r + ", " + g + ", " + b + ", .3)";
      let card = document.querySelector(".user-card");
      card.style.backgroundColor = newColor;
    },
    onImgLoad() {
      return (this.isLoaded = true);
    },
  },
  mounted() {
    this.getUser();
    this.randomColor();
  },
};
</script>
<style lang="sass" scoped>
.user-card
    display: flex
    margin: 10px auto
    flex-direction: row
    width: 500px
    border: solid 1px grey
    border-radius: 4px
    box-sizing: border-box
    padding: 5px
    box-shadow: 1px 1px 10px rgba(0,0,0,.5)
    @media screen and (max-width: 680px)
      width: 100%
.user-card__info
    display: flex
    flex-direction: column
    margin-top: 10px
.user-card__pict-container
    display: block
    border: solid 1px transparent
    box-sizing: border-box
    margin-right: 20px
.user-card__pict
    width: 200px
    border-radius: 50%
    @media screen and (max-width: 680px)
      width: 150px
    @media screen and (max-width: 460px)
      width: 100px
.user-card__stroke
    line-height: 2
    text-align: left
    font-size: 14px
    @media screen and (max-width: 460px)
      font-size: 12px
</style>
