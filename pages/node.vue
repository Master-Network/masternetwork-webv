<template>
  <div>
    <v-app>
      <v-app-bar app>
        Masternetwork
        <v-layout justify-end>
          <v-card-actions>
            <v-btn color="success" class="mr-4" @click="REGISTER">
              Register
            </v-btn>
            <v-btn color="error" class="mr-4" @click="LOGIN"> Login </v-btn>
          </v-card-actions>
        </v-layout>
      </v-app-bar>
<img src="/dc.jpg" max-width="400px" class="mx-auto">
      <v-main class="ma-8"  max-width="500" min-width="350">
        
        <p  max-width="500">
          Becoming a node means hosting virtual machines (VPS) in exchange for
          crypto currency for others. It's very easy to set up and can allow you
          to earn cryptocurrency by making available your servers that you don't
          use. 
          <br><br>
          However, you will need a very good internet connection and
          reliability (it should be very rare that a user is unable to connect
          to his instance).
          <br><br>
          For now, your hardware must be based on ubuntu or debian, and will require sudo rights to run. Indeed, the program installs dependencies during its operation allowing the administration of virtual machines.
          <br><br>
          You can, in a few minutes, start a node by following our <a href="https://docs.masternetwork.dev/installation">guide</a>. On demand, virtual machines will be broken up and from that moment on you will start earning cryptocurrency. 
          You can choose what you allocate in terms of resources (vcpus, ram, storage.
        </p>
      </v-main>
    </v-app>

    <div>
      <v-layout justify-center>
        <v-card-actions>
          <v-btn color="" class="mr-4 text-center" fluid>
            <a href="https://docs.masternetwork.dev"> Documentation </a>
          </v-btn>
        </v-card-actions>
      </v-layout>
    </div>
    <v-text
      class="float-left ma-8"
      width="344"
      shaped
      v-for="mountain of mountains"
      :key="mountain.Workers"
    >
      Number of current users : {{ mountain.users * 2 }} <br /><br />
    </v-text>
  </div>
</template>
<script>
export default {
  head() {
    return {
      title: "Become a node - Masternetwork",
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: "Becoming a node",
          name: "Becoming a node",
          content: "Becoming a node",
        },
      ],
    };
  },

  mounted() {
    console.log(this.$route.query.sponsor);
  },
  async fetch() {
    this.mountains = await fetch("https://api.masternetwork.dev/stats/").then(
      (res) => res.json()
    );
  },
  layout: "plain2",
  methods: {
    REGISTER() {
      this.$router.push("/auth/signup");
    },
    LOGIN() {
      this.$router.push("/login");
    },
  },
};
</script>