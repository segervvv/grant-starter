<template>
  <v-app ma="0" pa="0" class="achtergrond">
    <!--    <transition-->
    <!--      enter-active-class="animate__animated animate__slideInLeft"-->
    <!--      appear-->
    <!--    >-->
    <router-view />
    <!--    </transition>-->
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      tokkie: null,
    };
  },
  created() {
    this.tokkie = this.$route.query.name;
    localStorage.setItem("tokkie", JSON.stringify(this.tokkie));
  },
};
</script>
<style>
html,
body {
  overflow-x: hidden;
}
.full-page {
  height: 250vh;
}
</style>
