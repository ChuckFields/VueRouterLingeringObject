<template>
  <div class="about">
    <button @click="goHome">Go Home</button>
    <h1>This is an about page</h1>
  </div>
</template>
<script>
import LingeringObject from "../model/LingeringObject.js";

export default {
  name: 'about',
  mounted() {
    this.$store.dispatch("setLingeringObj", new LingeringObject({
      id: Math.floor((Math.random() * 100000) + 1)
    }));
  },
  beforeDestroy() {
    console.log("About- beforeDestroy()");
  },
  watch: {
    '$store.state.lingeringObj': function () {
      console.log('lingeringObj changed!')
    }
  },
  methods: {
    goHome() {
      this.$router.push('/');
    }
  },
  beforeRouteLeave(to, from, next) {
    this.$store.dispatch("setLingeringObj", null);
    next();
  },
}
</script>
