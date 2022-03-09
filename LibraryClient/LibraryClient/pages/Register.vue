<template>
<b-container fluid="md" class="mt-5 mb-5">
    <b-row>
      <b-col md="12">
        <b-card class="shadow-md border-0 rounded-lg">
           <h2 class="title is-3 has-text-grey">
      Login 
    </h2>
    <section>
        <b-field label="Email">
            <b-input type="email"
                maxlength="30">
            </b-input>
        </b-field>
        <b-field label="Username">
            <b-input type="text"
                maxlength="30">
            </b-input>
        </b-field>

        <b-field label="Password">
            <b-input type="password" maxlength="30"></b-input>
        </b-field>
       <b-button type="submit" variant="primary" @click="Register()">Register</b-button>
        
    </section>
    </b-card>
     </b-col>
    </b-row>
  </b-container>
</template>
<script>
export default {
  name: 'RegisterUser',
  methods: {
  async registerUser() {
    this.loading = true;
    const data = this.register;
    try {
      await this.$axios.post("/user/create", data);
      this.$router.push("/login");
      this.loading = false;
      this.$notify({
        group: "success",
        title: "Success!",
        text: "Account created successfully"
      });
    } catch (error) {
      this.loading = false;
      this.$notify({
        group: "error",
        title: "Error!",
        text: error.response
          ? error.response.data.error
          : "Sorry an error occured, check your internet"
      });
    }
  }
}
}</script>