<template>
<div>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline"> User Profile </v-card-title>
        <v-card-text>
          <p>Your e-mail is {{ user ? user.email : "" }}</p>
          <div v-for="u of udata" :key="u.uid">
          balance : {{ u.xmr_balance }} xmr <br><br>
          api key : "{{ u.api_key }}" <br><br>
          xmr_subadress: {{ u.xmr_subadress}} <br><br>
          </div>
          <v-btn @click="logout">Logout</v-btn>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
  
</div>

</template>

<script>
import axios from 'axios';
import { mapState } from "vuex";
export default {
  
  computed: {
    ...mapState(["user"]),
   
  },
  methods: {
    async logout() {
      await this.$fire.auth.signOut();
      this.$router.replace("/");
      
    },
  },
  
    data() {
      return {
        udata: []
      }
    },
    mounted() {
    console.log(process.env.TEST_VARIABLE)
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