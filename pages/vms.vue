<template>
  <div>
    <p v-if="$fetchState.pending">Loading....</p>
    <p v-else-if="$fetchState.error">Error while fetching vms</p>

    <div v-for="(mountain, index) in mountains" :key="index">
      <v-card elevation="2" v-if="mountain.Statewanted != -42">
        <v-card-title>
          {{ mountain.name }}
          <v-row justify="end">
            <v-card-actions>
              <v-btn
                class="ma-2"
                color="primary"
                dark
                v-on:click="startVM(mountain.key)"
                :loading="loading && index == i"
                @click="
                  loader = 'loading';
                  i = index;
                "
              >
                Start
                <v-icon dark right> mdi-checkbox-marked-circle </v-icon>
              </v-btn>
              <v-btn
                class="ma-2"
                color="red"
                dark
                v-on:click="stopVM(mountain.key)"
                :loading="loading && index == i"
                @click="
                  loader = 'loading';
                  i = index;
                "
              >
                Stop
                <v-icon dark right> mdi-cancel </v-icon>
              </v-btn>
            </v-card-actions>
          </v-row>
        </v-card-title>

        <v-card-subtitle>Type: {{ mountain.instancetype }}</v-card-subtitle>

        <v-card-text>
          mode: {{ mountain.mode }} <br />
          State: <span v-if="mountain.State == 1">Running</span>
          <span v-else>
            <span v-if="mountain.State == -69">In creation</span>
            <span v-if="mountain.State == 0">Starting</span>
          </span>
          <br />
          password: {{ mountain.password }} <br />
          Order executed:
          <span v-if="mountain.OrderFilled == 'true'">Yes</span>
          <span v-else>Not yet</span> <br />
        </v-card-text>
        <v-card-actions>
          <v-row justify="space-around">
            <v-btn
              pressed
              color="primary"
              v-if="detail == false"
              v-on:click="detail = true"
            >
              Configuration
              <v-icon dark right> mdi-cog-outline </v-icon>
            </v-btn>
            <v-btn
              pressed
              color="primary"
              v-if="detail == true"
              v-on:click="detail = false"
            >
              Configuration
              <v-icon dark right> mdi-cog-outline </v-icon>
            </v-btn>
            <v-btn
              pressed
              color="error"
              v-on:click="deleteVM(mountain.key)"
              v-if="mountain.Statewanted != -69"
              depressed
              disabled
            >
              Delete
              <v-icon dark right> mdi-delete </v-icon>
            </v-btn>
            <v-btn
              pressed
              color="error"
              v-on:click="deleteVM(mountain.key)"
              v-else
            >
              Delete
              <v-icon dark right> mdi-delete </v-icon>
            </v-btn> </v-row
          ><br /><br />
        </v-card-actions>
        <v-card-text v-if="detail == true">
          <v-btn
            pressed
            color="primary"
            v-if="Editing == false"
            v-on:click="Editing = true"
          >
            <v-icon dark right> mdi-pen-plus </v-icon>
          </v-btn>
          <v-btn pressed color="primary" v-else v-on:click="Editing = false">
            <v-icon dark right> mdi-pen-plus </v-icon>
          </v-btn>

          <div v-if="Editing == true">
            <v-form ref="form" v-model="valid" lazy-validation>
              <v-text-field
                v-model="name"
                :counter="50"
                label="Name or Custom domain"
                required
              ></v-text-field>

              <v-text-field
                v-model="localport"
                :counter="5"
                label="Local Port"
                type="number"
                required
              ></v-text-field>

              <v-select
                v-model="type"
                :items="Types"
                :rules="[(v) => !!v || 'Type is required']"
                label="Type"
                required
              ></v-select>

              <v-btn
                :disabled="!valid"
                color="success"
                class="mr-4"
                @click="validate(mountain.key)"
              >
                Validate
              </v-btn>
            </v-form>
          </div>
          <hr />
          <span v-for="(port, index) in ports" :key="index">
            <span v-if="port.key == mountain.key">
              <br />

              name: {{ port.portname }} <br />
              type: {{ port.type }}<br />
              localport: {{ port.localport }} <br />
              <span v-if="port.remoteport != null"
                >remote port: {{ port.remoteport }}</span
              >
              <br />
              <v-btn
                pressed
                right
                color="error"
                v-on:click="deleteport(port._id.$oid)"
              >
                Delete
                <v-icon dark right> mdi-delete </v-icon>
              </v-btn>
              <span v-if="port.portsupdated == false"
                >Port not applied for now</span
              >
              <br />
              <hr />
            </span>
          </span>
        </v-card-text>
      </v-card>
      <br />
      <br />
    </div>
    Create a new virtual machine
    <br />

    <br />
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-select
        v-model="type"
        :items="items"
        label="Instance type"
        required
      ></v-select>
      <v-text-field
        v-model="name"
        :rules="nameRules"
        label="name"
        required
      ></v-text-field>

      <v-btn color="success" class="mr-4" @click="SEND"> Validate </v-btn>
    </v-form>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";
export default {
  computed: {
    ...mapState(["user"]),
  },
  data: () => ({
    Types: ["tcp", "customdomain"],

    Editing: false,
    detail: false,
    index: -1,
    loader: null,
    loading: false,
    mountains: [],
    items: ["C1"],
    valid: true,
    adress: "",
    snackbar: false,
    errorMessage: "",
  }),

  methods: {
    SEND() {
      const axios = require("axios");
      console.log(this.$fire.auth.currentUser.uid);
      console.log(this.name);
      axios.get(
        "https://api.masternetwork.dev/newvmONDEMAND/" +
          this.name +
          "/" +
          this.type +
          "/" +
          this.$fire.auth.currentUser.uid
      );
    },
    validate(key) {
      const axios = require("axios");
      //{name}/{localport}/{type}/{key}/
      axios.get(
        "https://api.masternetwork.dev/newport/" +
          this.name +
          "/" +
          this.localport +
          "/" +
          this.type +
          "/" +
          key
      );
    },
    deleteVM(key) {
      if (
        confirm(
          "This action isn't recoverable. Are you sure you want to delete ?"
        )
      ) {
        const axios = require("axios");
        axios.get("https://api.masternetwork.dev/deletevm/" + key);
      }
    },
      deleteport(doc) {
      if (
        confirm(
          "This action isn't recoverable. Are you sure you want to delete ?"
        )
      ) {
        const axios = require("axios");
        axios.get("https://api.masternetwork.dev/deleteport/" + doc);
      }
    },
    startVM(key) {
      const axios = require("axios");
      axios.get("https://api.masternetwork.dev/startvm/" + key);
    },
    stopVM(key) {
      const axios = require("axios");
      axios.get("https://api.masternetwork.dev/stopvm/" + key);
    },
  },

  async fetch() {
    this.mountains = await fetch(
      "https://api.masternetwork.dev/listVM/" + this.$fire.auth.currentUser.uid
    ).then((res) => res.json());
    console.log(this.mountains);
    this.ports = await fetch(
      "https://api.masternetwork.dev/ListPORTS/" +
        this.$fire.auth.currentUser.uid
    ).then((res) => res.json());
    console.log(this.ports);
  },
  watch: {
    loader() {
      const l = this.loader;
      this[l] = !this[l];

      setTimeout(() => (this[l] = false), 500);

      this.loader = null;
    },
  },
};
</script>

<style>
</style>