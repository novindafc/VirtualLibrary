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

        <b-field label="Password">
            <b-input type="password" maxlength="30"></b-input>
        </b-field>
       <b-button type="submit" variant="primary" @click="logIn()">Log in</b-button>
        
    </section>
    </b-card>
     </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  name: 'LoginUser',
  layout: "empty",
  data(){
    return{
      email:'',
      password:'',
    }
    
  },
  
  methods: {
  async logIn() {
    
    const data = this.login;
    this.loading = true;
    try {
      const res = await this.$auth.loginWith("local", {
        data
      });
      this.loading = false;
      const user = res.data.data.user;
      this.$auth.setUser(user);
      this.$notify({
        group: "success",
        title: "Success!",
        text: "Welcome!"
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
}

</script>