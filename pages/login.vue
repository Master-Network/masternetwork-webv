<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="4">
      <v-form ref="form" v-model="valid" lazy-validation @submit.prevent="">
        <v-text-field
          v-model="email"
          :rules="emailRules"
          type="email"
          label="E-mail"
          autocomplete="username"
          required
        ></v-text-field>

        <v-text-field
          v-model="password"
          :rules="passwordRules"
          type="password"
          label="Password"
          autocomplete="current-password"
          required
        ></v-text-field>

        <v-btn :disabled="!valid" color="success" class="mr-4" @click="login">
          Login
        </v-btn>

        <v-btn color="success" class="mr-4" @click="forgetPassword">
          Forget Password
        </v-btn>
         <v-btn color="success" class="mr-4" @click="REGISTER">
          Register
        </v-btn>
      </v-form>

      <v-snackbar v-model="snackbar" color="error">
        {{ errorMessage }}
      </v-snackbar>
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: "plain",
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 10) || "Name must be less than 10 characters long",
    ],
    password: "",
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => (v && v.length >= 6) || "Password must be at least 6 characters long",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    snackbar: false,
    errorMessage: "",
  }),

  methods: {
    login() {
      let formValidation = this.$refs.form.validate();

      if (formValidation) {
        this.$fire.auth
          .signInWithEmailAndPassword(this.email, this.password)
          .then((userCredential) => {
            const authUser = {
              uid: userCredential.user.uid,
              email: userCredential.user.email,
            };
            this.$store
              .dispatch("onAuthStateChangedAction", {
                authUser,
              })
              .then(() => {
                const axios = require('axios');
                axios.get('https://api.masternetwork.dev/login/'+authUser.uid)
                this.$router.replace("/profile");
              })
              .catch((error) => {
                console.log("User State error", error);
              });
          })
          .catch((error) => {
            console.log("Login error", error);
            this.snackbar = true;
            this.errorMessage = error.message;
          });
      }
    },
    forgetPassword() {
      console.log("clicked on forget password");
      this.$router.push("/auth/resetpassword");
    },
     REGISTER() {
      console.log("clicked register");
      this.$router.push("/auth/signup");
    },
  },
};
</script>
