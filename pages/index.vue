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

      <!-- Sizes your content based upon application components -->
      <v-main>
        <v-container grid-list-md text-xs-center>
          <v-layout row wrap>
            <v-flex>
              <v-card class="mx-auto" max-width="500" min-width="350">
                <v-list-item three-line>
                  <v-list-item-content>
                    <div class="text-overline mb-4">VPS</div>
                    <v-list-item-title class="text-h5 mb-1">
                      Virtual private servers
                    </v-list-item-title>
                    <v-list-item-subtitle
                      >Create a VPS in minutes. <br />Starting @ 0.005$ per
                      hour.
                    </v-list-item-subtitle>
                  </v-list-item-content>

                  <v-list-item-avatar tile size="80" color="grey">
                    <img src="/dc.jpg" alt="Datacenter @ VPS"
                  /></v-list-item-avatar>
                </v-list-item>

                <v-card-actions>
                  <v-btn outlined rounded @click="INSTANCE">Instance</v-btn>
                </v-card-actions>
              </v-card>
            </v-flex>
            <v-flex>
              <v-card class="mx-auto" max-width="500" min-width="350">
                <v-list-item three-line>
                  <v-list-item-content>
                    <div class="text-overline mb-4">Node</div>
                    <v-list-item-title class="text-h5 mb-1">
                      Become a Node
                    </v-list-item-title>
                    <v-list-item-subtitle
                      >Earn cryptocurrency by lending your server for
                      developpers.</v-list-item-subtitle
                    >
                  </v-list-item-content>

                  <v-list-item-avatar tile size="80" color="grey">
                    <img src="/nodebtc.jpg" alt="Datacenter @ VPS"
                  /></v-list-item-avatar>
                </v-list-item>

                <v-card-actions>
                  <v-btn outlined rounded text @click="NODE"> Start </v-btn>
                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>

        <v-container fluid>
          <v-row class="">
            <v-card-text>
              <h2>What is the masternetwork ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              The masternetwork is a platform that connects computing power with
              developers in exchange for cryptocurrency. <br />
              If you do not use a server supporting virtualization, a rasberry
              pi, you can make it available to the platform.<br />
              Thus, depending on the demand, your server will be able to run
              virtual machines for others and you will receive cryptocurrencies
              according to the computing power used
            </v-card-text>
            <v-card-text>
              <h2>How to start a virtual machine ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              Starting a virtual machine is very fast and it will be delivered
              within minutes if there are enough nodes available. For the moment
              there is only one type of instance, the C1 instances : 1vcpus,
              2048mb of ram, 10gb storage, ubuntu jammy for 0.005 $ an hour
            </v-card-text>

            <v-card-text>
              <h2>How to create a node ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              It's easy to setup, please check our
              <a href="https://docs.masternetwork.dev">documentation</a>
            </v-card-text>

            <v-card-text>
              <h2>What is the currency ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              We use monero, it's a private, decentralized cryptocurrency.
              <br />
              In order to fill your account with monero, you have to send monero
              to one of our subadress that is asign to you (you can collect it
              in your profile section). If you send monero, we will see that
              there is a new transaction and that will allow us to fill your
              account.<br />
              We would like, later, to add many others crypto currencies such as
              solana, bitcoin, ethereum.
              <br />
              We take a 30% commission between the node and the users.
            </v-card-text>

            <v-card-text>
              <h2>Need help ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              We will be happy to help you on our
              <a href="https://discord.gg/NVvvkXMbAB">discord</a> <br /><br />
            </v-card-text>
            <v-card-text>
              <h2>And ...</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              The user interface is open source on
              <a href="https://github.com/Parmicciano/remote-python-webv"
                >github</a
              >, feel free to improve it. All the actions you perform in the
              interface are available to be used directly with your api key @
              api.masternetwork.dev
              <br />
            </v-card-text>
            <v-card-text class="pa-md-4"> </v-card-text>
          </v-row>
          <!-- If using vue-router -->
          <router-view></router-view>
        </v-container>
      </v-main>

      <v-footer app>
        <!-- -->
      </v-footer>
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
      Number of current users : {{ mountain.users * 3 }} <br /><br />
    </v-text>
  </div>
</template>
<script>
export default {
  head() {
    return {
      title: "The Masternetwork - A User Federated Cloud",
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        {
          hid: "A User Federated Cloud",
          name: "A User Federated Cloud",
          content: "A User Federated Cloud",
        },
      ],
    };
  },

  data() {
    return {
      mountains: [],
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
    INSTANCE() {
      this.$router.push("/vps");
    },
     NODE() {
      this.$router.push("/node");
    }
  },
};
</script>
