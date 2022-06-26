<template>
  <div>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-card-title class="headline">Your Portfolio</v-card-title>
          <v-card-text>
            <div v-for="u of udata" :key="u.uid">
              Monero balance : {{ u.xmr_balance }} xmr <br /><br />
              Send your monero to this subadress to fill your portfolio.<br><br>
              address : {{ u.xmr_subadress }} <br /><br />
              <figure class="qrcode">
                <qr-code :text="u.xmr_subadress" error-level="H"></qr-code>
                <img
                  class="qrcode__image"
                  src="https://www.getmonero.org/press-kit/symbols/monero-symbol-1280.png"
                  alt="Chen Fengyuan"
                />
              </figure>
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <vue-qrcode value="Hello, World!"></vue-qrcode>
    <br />
    <br />
    Send all your monero to your adress
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="adress"
        :counter="95"
        :rules="nameRules"
        label="Your adress"
        required
      ></v-text-field>

      <v-checkbox
        v-model="checkbox"
        :rules="[(v) => !!v || 'You must be sure to continue !']"
        label="Sure ?"
        required
      ></v-checkbox>

      <v-btn :disabled="!valid" color="success" class="mr-4" @click="SEND">
        Validate
      </v-btn>
    </v-form>

    <v-card
      class="float-left ma-8 d-none"
      width="344"
      shaped
      v-for="mountain of mountains"
      :key="mountain.path"
      hidden
    >
      <v-card-text>
        <p class="text-h4 text--primary">
          {{ mountain.oldname }}
        </p>
        xmr_per_sec :{{ mountain.xmr_per_sec }}
        <div class="text--primary"></div>
      </v-card-text>
      <v-card-actions>
        <v-btn
          text
          color="blue darken-2 accent-4"
          @click="deleted(mountain.path)"
          >delete
        </v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";
import Vue from "vue";
import VueQRCodeComponent from "vue-qrcode-component";
Vue.component("qr-code", VueQRCodeComponent);
export default {
  computed: {
    ...mapState(["user"]),
  },
  data: () => ({
    qrsub: localStorage.getItem("qrcode"),
    udata: [],
    valid: true,
    adress: "",
    nameRules: [
      (v) => !!v || "adress is required",
      (v) => (v && v.length > 10) || "adress must be bigger than 10 characters",
    ],
    password: "",
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => (v && v.length >= 6) || "Password must minimums 6 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    qrCls: "qrcode",
    qrText: "Read VueJS Feed daily",
    size: 500,
    background: "#E91E63",
    snackbar: false,
    errorMessage: "",
  }),

  methods: {
    SEND() {
      const axios = require("axios");
      console.log(this.$fire.auth.currentUser.uid);
      console.log(this.adress);
      axios.get(
        "https://api.masternetwork.dev/payment/send/" +
          this.$fire.auth.currentUser.uid +
          "/{useradress}?usradress=" +
          this.adress
      );
    },
  },
  async fetch() {
    this.udata = await fetch(
      "https://api.masternetwork.dev/login/" + this.$fire.auth.currentUser.uid
    ).then((res) => res.json());
    console.log(this.udata);
  },
};
</script>

<style scoped>
.qrcode {
  display: inline-block;
  font-size: 0;
  margin-bottom: 0;
  position: relative;
}

.qrcode__image {
  background-color: #fff;
  border: 0.25rem solid #fff;
  border-radius: 0.25rem;
  box-shadow: 0 0.125rem 0.25rem rgba(0, 0, 0, 0.25);
  height: 25%;
  left: 50%;
  overflow: hidden;
  position: absolute;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 25%;
}
</style>