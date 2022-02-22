<template>
<div>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">Monero</v-card-title>
        <v-card-text>
          <div v-for="u of udata" :key="u.uid">
          balance : {{ u.xmr_balance }} xmr <br><br>
          xmr_subadress: {{ u.xmr_subadress}} <br><br>
          </div>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
  <br>
  <br>
  Send all your monero to your adress
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="adress"
      :counter="95"
      :rules="nameRules"
      label="Your adress"
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






<v-card
    class="float-left ma-8 d-none"
    width="344"
   shaped v-for="mountain of mountains" :key="mountain.path" hidden>
    <v-card-text>


      <p class="text-h4 text--primary">
       {{ mountain.oldname }} 
      </p>
      xmr_per_sec :{{ mountain.xmr_per_sec }} 
      <div class="text--primary">
    time to do : {{ mountain.time_to_do }}
    <br>
    times done : {{ mountain.time_done }} 
    <br>
    times left : {{ mountain.time_to_do - mountain.time_done }}
      </div>

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
import axios from 'axios';
import { mapState } from "vuex";
export default {
  
  computed: {
    ...mapState(["user"]),
   
    },
  data: () => ({
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
    snackbar: false,
    errorMessage: "",
  }),
  methods : {
      SEND() {
        const axios = require('axios');
        console.log(this.$fire.auth.currentUser.uid)
        console.log(this.adress)
        axios.get("https://api.masternetwork.dev/payment/send/"+this.$fire.auth.currentUser.uid+"/{useradress}?usradress="+this.adress)
        
      }
  },
    async fetch() {
      this.udata = await fetch(
        'https://api.masternetwork.dev/login/'+this.$fire.auth.currentUser.uid
      ).then(res => res.json())
      console.log(this.udata)


      this.mountains = await fetch(
        'https://api.masternetwork.dev/show/files/'+this.$fire.auth.currentUser.uid
      ).then(res => res.json())
      
    }

};

</script>

<style>
</style>