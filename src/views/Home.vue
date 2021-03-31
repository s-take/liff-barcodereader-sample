<template>
  <v-container>
    <v-row justify="center" v-if="isExBrowser" class="mt-8">
      <v-btn large color="success" @click="loginAction">ログイン</v-btn>
    </v-row>
    <v-row justify="center" v-if="!isClient" class="mt-8">
      <v-btn large color="success">JAN読み取り</v-btn>
    </v-row>
    <v-row justify="center" v-if="!isClient" class="mt-8">
      <v-btn large color="success" @click="gotoEx">外部ブラウザ</v-btn>
    </v-row>
    <ReadBarCode />
  </v-container>
</template>

<script>
import liff from "@line/liff";
import ReadBarCode from "../components/ReadBarCode.vue";

export default {
  name: "home",
  components: {
    ReadBarCode,
  },
  data() {
    return {
      name: "",
      accessToken: "",
      idToken: "",
      isClient: false,
      isExBrowser: false,
    };
  },
  created() {
    this.initializeLiff();
  },
  methods: {
    initializeLiff() {
      var me = this;
      // eslint-disable-next-line
      liff
        .init({
          liffId: process.env.VUE_APP_LIFF_ID,
        })
        // eslint-disable-next-line
        .then(() => {
          // eslint-disable-next-line
          if (liff.isLoggedIn()) {
            me.isClient = liff.isInClient();
            if (me.isClient) {
              liff.openWindow({
                url: "https://liff.line.me/1655812015-N2OZAbge",
                external: true,
              });
            }
            me.accessToken = liff.getAccessToken();
            me.idToken = liff.getIDToken();
            // ログイン済み
          } else {
            me.isExBrowser = true;
            liff.login();
          }
        })
        .catch((err) => {
          // eslint-disable-next-line
          console.log("LIFF initialization failed", err);
        });
    },
    gotoEx() {
      liff.openWindow({
        url: "https://liff.line.me/1655812015-N2OZAbge",
        external: true,
      });
    },
    loginAction: function() {
      // ログインまだ
      // LINEブラウザはlogin不要
      // eslint-disable-next-line
      if (!liff.isLoggedIn()) {
        // eslint-disable-next-line
        liff.login();
      }
    },
  },
};
</script>
