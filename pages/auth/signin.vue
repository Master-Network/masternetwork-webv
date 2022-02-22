<template>
<div>
  <div><h1>Sign in page</h1></div>

</div>
</template>

<script>
export default {
  beforeCreate() {
    console.log(
      "In Signin page - this.$fire.auth",
      this.$fire.auth.currentUser
    );
   
    if (this.$fire.auth.currentUser) {
      this.$router.replace("/");
    };
  },
};
</script>

<style>
</style>
