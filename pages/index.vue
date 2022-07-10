<template>
  <div>
    <v-app>
      <v-app-bar app>
        <a href="https://masternetwork.dev">Masternetwork</a>
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
              The masternetwork is a FOSS platform that allows people to give up
              computing power for developers in exchange for cryptocurrency. The
              portion/s of computing power given up by people are called
              "nodes". If you choose to give up computing power on a device not
              supporting virtualization e.g a raspberry pi, you can make the
              whole device available to the platform. Thus, depending on demand
              for computing power, your server/device will be able to run
              virtual machines for others. In exchange, you will receive Monero,
              the amount depending on the time your computing power was used and
              how much of it. Essentially, it is a crowd-sourced,
              semi-decentralized VPS platform that allows developers to rent a
              VPS but without relying on a single company.
            </v-card-text>

            <v-card-text>
              <h2>How to create a node ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              It's easy to setup, please check our
              <a href="https://docs.masternetwork.dev">documentation</a>
            </v-card-text>

            <v-card-text>
              <h2>What currency do we use?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              We use Monero, a private, decentralized, untraceable
              cryptocurrency. Monero uses many technologies to ensure security
              and privacy unlike (arguably) any other cryptocurrency. To find
              out more please visit https://www.getmonero.org/ . In order to
              fill your account with Monero which can be used for purchasing
              your own decentralized VPS, you have to send monero to a
              custom-generated Monero address specific to your account. You can
              find this in the profile section of your masternetwork account. If
              you send Monero to this address and it goes through (5-10mins), we
              will then credit your account with the Monero. If you are looking
              to purchase a masternetwork VPS with a different cryptocurrency,
              we sadly do not yet have that available however we are looking to
              support other cryptocurrencies in the future e.g zcash, ethereum,
              or bitcoin. We take a 30% commission between the nodes and the
              users. Need help ? We will be happy to help you on our discord
              found here.
            </v-card-text>
            <v-card-text>
              <h2>
                Security: How do I know I am secure and safe while
                donating/using computing power on the masternetwork?
              </h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              We take your privacy and security very seriously at the
              masternetwork. We use several technologies to ensure your PII
              (personally identifiable information) ends up in nobody's hands.
              For this reason, we have a custom routing solution that ensures
              the node operators IP Address is not compromised. We also have a
              custom-developed API which due to security reasons is currently
              closed source, however we are looking into making it open source
              with time. With time, we are also planning on moving to Tor
              routing on both sides to ensure that sensitive activities are not
              leaked to the ISP, node operator, or anybody else.
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
              The UI is completely FOSS on
              <a href="https://github.com/Parmicciano/remote-python-webv"
                >github</a
              >; feel free to improve it. All the actions you perform in the
              interface are available to be used directly with your api key.
              found @ api.masternetwork.dev
              <br />
            </v-card-text>
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
      Number of current masternodes : {{ mountain.Workers * 3 }} <br /><br />
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
    },
  },
};
</script>
