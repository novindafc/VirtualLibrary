<template>
<b-container fluid="md" class="mt-5 mb-5">
    <b-row>
      <b-col md="12">
        <b-card class="shadow-md border-0 rounded-lg">
           <h2 class="title is-3 has-text-grey">
      Logout 
    </h2>
    </b-card>
     </b-col>
    </b-row>
  </b-container>
</template>
<script>

export default ({
    name:"logoutPage",
    setup() {
        window.location = 'http://localhost:3000/login'
    },
})
</script>
