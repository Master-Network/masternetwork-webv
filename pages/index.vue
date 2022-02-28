<template>
<div>
<v-container fluid>
  <v-layout justify-center align-center>
    <v-flex shrink>
            <img src="logo-dark.png">
    </v-flex>
  </v-layout>
</v-container>


<v-layout justify-end>
  <v-card-actions>
<v-btn color="success" class="mr-4" @click="REGISTER">
          Register
</v-btn>
<v-btn color="error" class="mr-4" @click="LOGIN">
          Login
</v-btn>
    </v-card-actions>
</v-layout>


<div>
<v-container fluid>
    <v-card>
       <v-row class="">

 <v-card-text>
           <h2>What is the masternetwork ?</h2>
  </v-card-text>
           <v-card-text class="pa-md-4">
The masternetwork allow developers to execute remotely their python script and to pay in monero.
If you have a computer that you don't use, you can get benefit from it by executing python script for others.
           </v-card-text>
 <v-card-text>
           <h2>How to run a python script ?</h2>
  </v-card-text>
           <v-card-text class="pa-md-4">
You can run a script by sending it to the network. <br>
You will have to define a price of execution per second (ex: 0.0000058 xmr per sec) and the number of repetition of the script (ex: I would like the script to run 5000 times).
You will pay only if your script work properly. <br>
You can see what dependencies you can use <a href="https://github.com/Parmicciano/Client-masternetwork/blob/master/client-repo-docker/requirements.txt">here</a>
<br><br>
Please make a request on <a href="https://discord.gg/NVvvkXMbAB">discord</a> in order to add some modules. 
           </v-card-text>

 <v-card-text>
           <h2>How to create a node ?</h2>
  </v-card-text>
           <v-card-text class="pa-md-4">
            It's easy to setup, please check our <a href="https://docs.masternetwork.dev">documentation</a>
           </v-card-text>

   <v-card-text>
           <h2>What is the currency ?</h2>
  </v-card-text>
           <v-card-text class="pa-md-4">
            We use monero, it's a private, decentralized cryptocurrency. 
            <br>
            In order to fill your account with monero, you have to send monero to one of our subadress that is asign to you (you can collect it in your profile section). If you send monero, we will see that there is a new transaction and that will allow us to fill your account.
            <br>
            If you have let your computer work and you want your monero, we can send it to you if its over 0.003 xmr. Otherwise you will basically just paying fees, that will not worth it. 
            <br>
            Remember that it's a cryptocurrency and so a transaction can take time.
<br> We take a 10% commission between the script reward and the node.
           </v-card-text>

 <v-card-text class="pa-md-4">


</v-card-text>

    </v-row>
    </v-card>
</v-container>

<v-layout justify-center>
  <v-card-actions>
         <v-btn color="" class="mr-4 text-center" fluid>
           <a href="https://docs.masternetwork.dev">
          Documentation
          </a>
        </v-btn>
    </v-card-actions>
</v-layout>

</div>
<v-text
    class="float-left ma-8"
    width="344"
   shaped v-for="mountain of mountains" :key="mountain.Workers">



    Number of users : {{ mountain.users }} <br><br>
    
    Number of Workers : {{ mountain.Workers }} 

</v-text>
</div>    
</template>
<script>
export default {

    head() {
      return {
        title: "The Masternetwork - Execute your python script all around the world",
        meta: [
          // hid is used as unique identifier. Do not use `vmid` for it as it will not work
          {
            hid: 'Execute your python script all around the world',
            name: 'Execute your python script all around the world',
            content: 'Execute your python script all around the world'
          }
        ]
      }
    }, 

    data() {
      return {
        mountains: [],
      }
    },
        async fetch() {
      this.mountains = await fetch(
        'https://api.masternetwork.dev/stats/'
      ).then(res => res.json())
                },
    layout: "plain2",
    methods : {
      
       REGISTER() {
      this.$router.push("/auth/signup");
    },
       LOGIN() {
      this.$router.push("/login");
    },
    }
}
</script>
