<template>
  <div class="hello">
    <p>Hello!</p>
    <user />
    <p>We think you'll love this beer, right?</p>
    <beer />
  </div>
</template>

<script>
import User from "./User.vue";
import Beer from "./Beer.vue";

export default {
  name: "BeerForYou",
  components: {
    User,
    Beer,
  },
};
</script>
