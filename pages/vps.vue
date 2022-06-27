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
                <td>
                  <v-text-field
                    v-model="calories"
                    type="number"
                    label="Less than"
                  ></v-text-field>
                </td>
                <td colspan="4"></td>
              </tr>
          
          </v-data-table>
        </div>
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
       search: '',
  
        instances: [
          {
            name: 'C1',
            vcpus: 1,
            ram: 2048,
            storage: 10,
            os: "ubuntu 22.04",
            price: '0.005',
          },
        ],
      }
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
