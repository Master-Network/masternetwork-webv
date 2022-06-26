<template>
<div>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">Sponsor</v-card-title>
        <v-card-text>
          <div v-for="u of udata" :key="u.uid">
          Referral : {{ u.sponsor_api_key }}  <br><br>
          Set a Referral ! <br>
          Use the api_key of somebody to give him 6.9% of your expenses of the masternetwork
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
  <br>
  <br>

  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="referral"
      :counter="96"
      :rules="nameRules"
      label="Referral api key"
      required
    ></v-text-field>


    <v-checkbox
      v-model="checkbox"
      :rules="[v => !!v || 'You must be sure to continue !']"
      label="Sure ?" 
      required
    ></v-checkbox>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="SEND"
    >
      Validate
    </v-btn>
  </v-form>






</div>

</template>

<script>
import axios from 'axios';
import { mapState } from "vuex";
export default {
  
  computed: {
    ...mapState(["user"]),
   
    },
  data: () => ({
    valid: true,
    referral: "",
    nameRules: [
      (v) => !!v || "adress is required",
      (v) => (v && v.length > 10) || "api key must be bigger than 10 characters",
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
    snackbar: false,
    errorMessage: "",
  }),
  methods : {
      SEND() {
        const axios = require('axios');
        console.log(this.$fire.auth.currentUser.uid)
        console.log(this.adress)
        axios.get("https://api.masternetwork.dev/sponsorship/"+this.$fire.auth.currentUser.uid+"/{apikeysponsor}?api_key_sponsor="+this.referral)
        
      }
  },
    async fetch() {
      this.udata = await fetch(
        'https://api.masternetwork.dev/login/'+this.$fire.auth.currentUser.uid
      ).then(res => res.json())
      console.log(this.udata)


    }

};

</script>

<style>
</style>