<template>
  <div>
    <not-int />
    <v-row no-gutters>
      <v-col
        cols="12"
        md="6"
        class="leftPanel align-center"
        :class="{ 'full-page': $vuetify.breakpoint.mdAndUp }"
      >
        <v-row class="ma-16">
          <v-col cols="2"></v-col>
          <v-col cols="8">
            <v-img
              :src="
                require(`@/assets/core/just_logo_${
                  $vuetify.theme.dark ? 'light3' : 'dark3'
                }.png`)
              "
              max-height="1200px"
            />
          </v-col>
        </v-row>
        <v-row class="justify-center">
          <h2 class="textHeaderLeftPanel--text">Welkom bij Grant Thornton</h2>
        </v-row>
        <v-row class="justify-center mt-10">
          <h3 class="textHeaderLeftPanel--text">
            Liever een ander kleurschema klik op de knop
          </h3></v-row
        >
        <v-row class="justify-center mt-10">
          <div class="text-center">
            <v-btn class="textHeaderLeftPanel mb-10" @click="toggle_dark_mode">
              <v-icon left>mdi-theme-light-dark</v-icon>
              <span>Donker/Licht</span>
            </v-btn>
          </div>
        </v-row>
      </v-col>
      <v-col cols="12" md="6">
        <div class="ma-5 pa-0">
          <vimeo-player
            :video-id="vimeo.intro"
            class="embed-container"
            :options="{ responsive: true }"
          ></vimeo-player>

          <br />
          <div v-if="formal">
            Beste {{ firstNameClient }} {{ lastNameClient }}, <br />
            <br />
            {{ textData.formal.text_a }}
            <br />
            <br />
            {{ textData.formal.text_b }}
            <br />
            <br />
            {{ textData.formal.text_c }}
            <br />
            <br />
            {{ textData.formal.text_d }}
            <br />
            <br />
            {{ textData.formal.text_e }}
            <br />
            <br />
            {{ textData.formal.text_f }}
            <br />
            <br />
            <br />
            {{ firstNameUser }} {{ lastNameUser }}<br />
          </div>
          <div v-if="!formal">
            Beste {{ firstNameClient }} ,<br />
            <br />
            {{ textData.informal.text_a }}
            <br />
            <br />
            {{ textData.informal.text_b }}
            <br />
            <br />
            {{ textData.informal.text_c }}
            <br />
            <br />
            {{ textData.informal.text_d }}
            <br />
            <br />
            {{ textData.informal.text_e }}
            <br />
            <br />
            {{ textData.informal.text_f }}
            <br />
            <br />
            <br />
            {{ firstNameUser }} {{ lastNameUser }}<br />
          </div>
          <div class="text-end mr-15 mb-10 mt-15">
            <v-btn elevation="15" class="accent white--text" @click="start"
              >Ja</v-btn
            >
            <v-btn elevation="15" class="ml-7 white accent--text" @click="end"
              >Nee</v-btn
            >
          </div>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import vimeoData from "@/text/vimeo.json";
import AuthService from "@/services/AuthService";
import NotInt from "@/components/core/notInt";
import textData from "@/text/textAintro.json";

export default {
  name: "Intro",
  components: { NotInt },
  data() {
    return {
      companyName: null,
      firstNameUser: null,
      lastNameUser: null,
      firstNameClient: null,
      lastNameClient: null,
      formal: true,
      valid: true,
      vimeo: vimeoData,
      textData: textData,
    };
  },
  methods: {
    toggle_dark_mode: function () {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
      localStorage.setItem("dark_theme", this.$vuetify.theme.dark.toString());
    },
    sleep(ms) {
      return new Promise((resolve) => {
        setTimeout(resolve, ms);
      });
    },
    start() {
      this.$router.push({ name: "Login" });
    },
    async end() {
      // eslint-disable-next-line
      console.log("stop");
      const payloadLog = {
        clientId: JSON.parse(localStorage.getItem("clientId")),
      };
      try {
        // eslint-disable-next-line no-undef
        await EventBus.$emit("notInt", true);
        await this.sleep(3000);
        await AuthService.notInt(payloadLog);
        localStorage.removeItem("clientId");
        localStorage.removeItem("firstNameClient");
        localStorage.removeItem("lastNameClient");
        localStorage.removeItem("emailClient");
        localStorage.removeItem("firstNameUser");
        localStorage.removeItem("lastNameUser");
        localStorage.removeItem("formal");
        this.$router.push({ path: "/Start" });
      } catch (error) {
        // eslint-disable-next-line no-undef
        EventBus.$emit("errNotInt", true);
      }
    },
  },
  mounted() {
    const theme = localStorage.getItem("dark_theme");
    if (theme) {
      this.$vuetify.theme.dark = theme === "true";
    }
    this.firstNameUser = JSON.parse(localStorage.getItem("firstNameUser"));
    this.lastNameUser = JSON.parse(localStorage.getItem("lastNameUser"));
    this.firstNameClient = JSON.parse(localStorage.getItem("firstNameClient"));
    this.lastNameClient = JSON.parse(localStorage.getItem("lastNameClient"));
    this.formal = JSON.parse(localStorage.getItem("formal"));
  },
  computed: {},
};
</script>

<style scoped></style>
