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
      <v-main class="ma-2">
        <span>
          Here are the different instances currently available. The "C"
          instances are intended to be used for computing, database
          administration, hosting websites and running scripts. Please tell us
          on <a href="https://discord.gg/NVvvkXMbAB">discord</a> the new
          instances you would like to see.
        </span>
        <br /><br />
        <div>
          <v-data-table
            :headers="headers"
            :items="instances"
            item-key="name"
            class="elevation-1"
            :search="search"
            :custom-filter="filterOnlyCapsText"
          >
            <template v-slot:top>
              <v-text-field
                v-model="search"
                label="Search"
                class="mx-4"
              ></v-text-field>
            </template>

            <tr>
              <td></td>
              <td></td>
              <td colspan="4"></td>
            </tr>
          </v-data-table>
        </div>
        <br /><br />
        <span>
        VPS is a term that may sound mystical, but in hindsight you will find that it is a simple technology to understand. Virtual Private Server is a technique implemented by web hosting companies to enable any entity to have multiple servers that allow them to manage their web activities more efficiently.

Because these servers are virtual, site management is more efficient and much more reliable in terms of security. The virtual private server works like the classic server, with one detail: it coexists with other virtual private servers on the same computer.
<br>
          Unfortunately, these instances don't work exactly like the ones you
          could use at AWS or Google Cloud. Indeed, the instances are hosted on
          servers belonging to individuals (homelab). This allows to provide
          lower prices and to exploit computing power usually not used. However,
          the instances are protected behind a firewall, so if you want to
          exploit a port such as 80 to expose a website, you will have to go on
          your interface and declare a domain name. By using CNAME in the dns
          records, you will be able to send your traffic directly to your
          instance.<br /><br />
          VPS is a common hosting model that is part of the Infrastructure as a Service (IaaS) services offered by many ISPs.VPS uses the resources of a physical server to provide users with the same It can be defined as a virtual machine (VM for short) that provides functionality. A VPS therefore represents the same concept as a VDS (Virtual Dedicated Server).

In commercial web hosting, multiple VPS servers are typically hosted on physical high-performance machines, each with its own operating system (OS) and giving users full root access rights. This allows each server administrator to operate independently of other users on the same hardware. Hardware is managed through a hypervisor: the virtual machine administrator. It is an application for creating and managing virtual machines. The hypervisor defines the virtual environment and provides some of the physical resources such as CPU (central processing unit), RAM (random access memory) and disk space for each virtual server. Root permissions allow VPS users to install all applications supported by the operating system of their choice. These can include web server software, email servers and certain e-commerce applications and blog systems.
<br><br>
          It works the same way for other ports, like port 3306 for example
          (mysql). You will just have to specify the port to your database
          connection tool (remote port).
          <br /><br />
          For more details about ordering a virtual private server, you can read
          our
          <a href="https://docs.masternetwork.dev/create-a-vm">documentation</a>
        </span>
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
      search: "",

      instances: [
        {
          name: "C1",
          vcpus: 1,
          ram: 2048,
          storage: 20,
          os: "ubuntu 22.04",
          price: "0.0075",
        },
        {
          name: "C2",
          vcpus: 2,
          ram: 4096,
          storage: 20,
          os: "ubuntu 22.04",
          price: "0.014",
        },
        {
          name: "C3",
          vcpus: 3,
          ram: 6144,
          storage: 25,
          os: "ubuntu 22.04",
          price: "0.0225",
        },
        {
          name: "C4",
          vcpus: 5,
          ram: 10000,
          storage: 50,
          os: "ubuntu 22.04",
          price: "0.0375",
        },
        {
          name: "C5",
          vcpus: 8,
          ram: 12000,
          storage: 75,
          os: "ubuntu 22.04",
          price: "0.08",
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
  computed: {
    headers() {
      return [
        {
          text: "Instance type",
          align: "start",
          sortable: true,
          value: "name",
        },

        { text: "vcpus", value: "vcpus" },
        { text: "ram (mb)", value: "ram" },
        { text: "Storage (gb)", value: "storage" },
        { text: "os", value: "os" },
        { text: "price ($)", value: "price" },
      ];
    },
  },
  methods: {
    filterOnlyCapsText(value, search, item) {
      return (
        value != null &&
        search != null &&
        typeof value === "string" &&
        value.toString().toLocaleUpperCase().indexOf(search) !== -1
      );
    },
    REGISTER() {
      this.$router.push("/auth/signup");
    },
    LOGIN() {
      this.$router.push("/login");
    },
  },
};
</script>
