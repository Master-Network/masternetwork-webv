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
<v-card
    class="float-left ma-8"
    width="344"
   shaped v-for="mountain of mountains" :key="mountain.folderid">
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
        @click="deleted(mountain.folderid)"
      >delete
      </v-btn>
    </v-card-actions>
    response : {{ deleteResponse }}
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
  methods: {
    
    async deleted(folderid) {
      console.log(folderid)
    	let deleteResponse  = await axios.get( 'https://api.masternetwork.dev/delete/'+folderid)
      this.deleteResponse = deleteResponse["data"]["response"]
      console.log(deleteResponse)
    },
    async logout() {
      await this.$fire.auth.signOut();
      this.$router.replace("/");
      
    },
  },
  
    data() {
      return {
        mountains: [],
        deleteResponse: ""
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


      this.mountains = await fetch(
        'https://api.masternetwork.dev/show/files/'+this.$fire.auth.currentUser.uid
      ).then(res => res.json())
      
    }

};

</script>

<style>
</style>