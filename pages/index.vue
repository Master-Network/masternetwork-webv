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
              VPS but without relying on a single company. <br />It is a cloud
              allowing above all the connection of suppliers of servers,
              machines and storage with operators / developers. Eventually, we
              want to make our machine services very efficient, with a billing
              based on machine performance (uptimes, network connectivity,
              resources). Also, we aim to build a very powerful CDN, based on
              the decentralization of servers, allowing then, an extremely fast
              access to the sites and services to consult. It would be great to
              create an alternative to Netlify by being semi-decentralized! We
              could then make the production of websites very fast and
              replicating to the four corners of the world in a few seconds.
              Moreover, since a website consumes very few resources, we can
              easily imagine that each node of the network could host a hundred
              websites in a few seconds and the users would not see any change
              if the node falls since the website would already be in production
              on hundreds of other servers! More complex this time but still
              quite interesting, we think it would be cool to create an S3
              server allowing users to store and retrieve content in a reliable
              and durable way (we could also allow users to determine their
              replication rate like 3,4 or 10, 50 or even 100 times!) Finally, I
              would like to develop a system allowing users to create their own
              network that they could use for themselves. The masternetwork
              would give them an interface and an easy to use reverse proxy and
              create, stop and all the operations one has to do with a virtual
              machine would be simplified and done remotely. I wish you a very
              nice stay on the masternetwork !
            </v-card-text>

            <v-card-text>
              <h2>How to create a node ?</h2>
            </v-card-text>
            <v-card-text class="pa-md-4">
              It's easy to setup, please check our
              <a href="https://docs.masternetwork.dev">documentation</a>.
              The client that serves as a program to get a node up and running is open source. You can check that it is not a malware that would degrade the performance of your machine for some reason. A masternode when as we could call it, is part of the system, it is launched a bit like torrents.
A masternode is thus to allocate the resources of your machine to the system and thus to make profit with the other users of your machine against cryptocurrencies, it is the principle! 
In theory, it's a bit like if you own an aws datacenter and you rent it to individuals in the form of virtual machine, storage services, web hosting, apis, cloud function and much more (in development)
You do have to meet quality standards to be a masternode, but don't worry, we will set up a series of tests and adaptive billing in the future!

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
              leaked to the ISP, node operator, or anybody else. As far as
              security is concerned, the masternetwork does its best to ensure
              the security of both nodes and users rather than adding features.
              Virtual machines are about to be encrypted (in development) which
              will eventually make virtual machines impossible to exploit for
              malicious nodes, and so much the better! Finally, if you ever find
              potential security holes, we will be very happy if you let us know
              directly on github or discord. If you can create a patch directly
              and send it to github. Of course, we will check it but it will
              allow us to focus on adding functionality.Virtual machines are
              secured by a username and password but you are free to make a
              custom configuration by putting a ssh key or even disable all
              possible ways of connection (if you are mentally insane aka cool
              people). Open only the ports you need to expose on the internet.
              If you open ports you don't need, it increases the risk of getting
              hacked. It is therefore necessary to open the ports sparingly!
              Also, be careful what you install on your virtual machines. Some
              of the processes running on virtual machines could be viruses that
              would use your computing power to mine crypto currencies, steal
              your data... If you have any doubt, do not hesitate to delete your
              virtual machines and to recreate them since it is made for that.
              On the masternetwork, it costs you absolutely no more to delete
              and recreate a virtual machine. Let's say your service is an API
              for your sites. You can then write a shell / bash script to
              automate the installation, which allows you to launch your service
              in a few seconds, in complete safety! Above all, do not hesitate
              to encrypt the documents that require it.
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
