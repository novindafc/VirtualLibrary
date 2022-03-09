<template>
  <b-container fluid="md" class="mt-5 mb-5">
    <b-row>
      <b-col md="12">
        <b-card class="shadow-md border-0 rounded-lg">
           <h2 class="title is-3 has-text-grey">
      Edit Member 
    </h2>
          <hr>
          <b-form @submit="update">
            <b-form-group label="Member Name">
              <b-form-input type="text" v-model="member.Name" :class="{ 'is-invalid': validation.Name }"
                placeholder="Enter Member Name">
              </b-form-input>
              <div v-if="validation.Name" class="mt-2">
                <b-alert show variant="danger">{{ validation.Name[0] }}</b-alert>
              </div>
            </b-form-group>
              <b-form-group label="Member Gender">
              <b-form-input type="text" v-model="member.Gender" :class="{ 'is-invalid': validation.Gender }"
                placeholder="Enter Member Gender">
              </b-form-input>
              <div v-if="validation.Gender" class="mt-2">
                <b-alert show variant="danger">{{ validation.Gender[0] }}</b-alert>
              </div>
            </b-form-group>
         
              <b-form-group label="Menber Phone">
              <b-form-input type="text" v-model="member.Phone" :class="{ 'is-invalid': validation.Phone }"
                placeholder="Enter Member Phone">
              </b-form-input>
              <div v-if="validation.Phone" class="mt-2">
                <b-alert show variant="danger">{{ validation.Phone[0] }}</b-alert>
              </div>
            </b-form-group>
            
              <b-form-group label="Member Occupation">
              <b-form-input type="text" v-model="member.Occupation" :class="{ 'is-invalid': validation.Occupation }"
                placeholder="Enter Member Occupation">
              </b-form-input>
              <div v-if="validation.Occupation" class="mt-2">
                <b-alert show variant="danger">{{ validation.Occupation[0] }}</b-alert>
              </div>
            </b-form-group>

             <b-form-group label="Member Email">
              <b-form-input type="text" v-model="member.Email" :class="{ 'is-invalid': validation.Email }"
                placeholder="Enter Member Occupation">
              </b-form-input>
              <div v-if="validation.Email" class="mt-2">
                <b-alert show variant="danger">{{ validation.Email[0] }}</b-alert>
              </div>
            </b-form-group>
            <b-button type="submit" variant="primary">UPDATE</b-button>
          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  export default {
       name: 'editMember',
    data() {
      return {
        member: {
          Name: '',
          Gender: '',
          Phone: '',
          Occupation: '',
          Email: '',
        },
        
        validation: []
      }
    },
    mounted() {

      this.$axios.get(`/items/member/${this.$route.params.id}`)
        .then(response => {
            this.member.Name   = response.data.data.Name;
            this.member.Gender   = response.data.data.Gender;
            this.member.Phone   = response.data.data.Phone;
            this.member.Occupation   = response.data.data.Occupation;
            this.member.Email   = response.data.data.Email;
        })
    },
    methods: {
      async update(e) {
        e.preventDefault()
        await this.$axios.put(`/items/member/${this.$route.params.id}`, {
            name: this.member.Name ,
            gender: this.member.Gender ,
            phone: this.member.Phone ,
            occupation: this.member.Occupation,
            email: this.member.Email,
          })
          .then(() => {
            
        
            this.$router.push({
              name: 'post'
            })
          })
          .catch(error => {
      
            this.validation = error.response.data
          })
      }
    }
  }
</script>


