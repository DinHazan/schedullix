<template>
<section class="share-page" v-if="isShow">

    <h1>Share your page</h1>
    <section class="btns-share-container">
        <social-sharing :url="businessUrl" title="The Progressive JavaScript Framework" description="Intuitive, Fast and Composable MVVM for building interactive interfaces."
            quote="Vue is a progressive framework for building user interfaces." hashtags="vuejs,javascript,framework" twitter-user="vuejs"
            inline-template>
            <div>
                <network network="facebook">
                    <v-btn fab small dark color="indigo" title="Copy Business URL">
                        <v-icon dark>fab fa-facebook-square</v-icon>
                    </v-btn>
                </network>
                <network network="whatsapp">
                    <v-btn fab small dark color="green" title="Copy Business URL">
                        <v-icon dark>fab fa-whatsapp</v-icon>
                    </v-btn>
                </network>
            </div>
        </social-sharing>
        <v-btn fab small dark color="pink" title="Copy Business URL">
            <v-icon dark>fab fa-instagram</v-icon>
        </v-btn>
    </section>

        <section class="address-page-container">
            <h3>{{businessUrl}}</h3>
            <v-btn fab small dark color="indigo" title="Copy Business URL" v-clipboard:copy="businessUrl" >
                <v-icon dark>file_copy</v-icon>
            </v-btn> 
        </section>
        
    </section>

</template>

<script>
import { GETTER_BUSINESS_NAME } from "@/store/userModule.js";

import {
  eventBus,
  EVENT_TOGGLE_SHARE_MENU
} from "@/services/event-bus-service.js";

export default {
  name: "share-page-cmp",
  data() {
    return {
      isShow: false
    };
  },
  created() {
    eventBus.$on(EVENT_TOGGLE_SHARE_MENU, _ => {
      this.isShow = !this.isShow;
    });
  },
  methods: {},
  watch: {},
  computed: {
    businessUrl() {
      return `http://schedullix.herokuapp.com/${
        this.$store.getters[GETTER_BUSINESS_NAME]
      }`;
    }
  }
};
</script>

<style scoped lang="scss">
.share-page {
  background-color: #403b3bd9;

  height: 150px;
  color: white;
  font-size: 10px;
  position: fixed;
  z-index: 100;
  border-radius: 5px;

  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 10px;
}

.address-page-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

h3 {
  border: 1px solid black;
  padding: 8px;
  background-color: #bdbdbd47;
  border-radius: 3px;
}

h1 {
  font-size: 20px;
}
@media only screen and (min-width: 600px) {
  .share-page {
    max-width: 420px;
    left: 15px;
    bottom: 110px;
  }
}

@media only screen and (max-width: 600px) {
  .share-page {
    left: 0px;
    top: 80px;
    width: 100vw;
  }
}
</style>