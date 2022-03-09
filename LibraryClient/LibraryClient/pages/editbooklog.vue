<template>
  <b-container fluid="md" class="mt-5 mb-5">
    <b-row>
      <b-col md="12">
        <b-card class="shadow-md border-0 rounded-lg">
           <h2 class="title is-3 has-text-grey">
      Edit Book Log 
    </h2>
          <hr>
          <b-form @submit="update">
            <b-field label="Select datetime start">
        <b-datetimepicker v-model="member.StartTime"
            placeholder="Click to select...">

            <template #left>
                <b-button
                    label="Now"
                    type="is-primary"
                    icon-left="clock"
                    @click="datetime = new Date()" />
            </template>

            <template #right>
                <b-button
                    label="Clear"
                    type="is-danger"
                    icon-left="close"
                    outlined
                    @click="datetime = null" />
            </template>
        </b-datetimepicker>
    </b-field>
    <b-field label="Select datetime End">
        <b-datetimepicker v-model="member.EndTime"
            placeholder="Click to select...">

            <template #left>
                <b-button
                    label="Now"
                    type="is-primary"
                    icon-left="clock"
                    @click="datetime = new Date()" />
            </template>

            <template #right>
                <b-button
                    label="Clear"
                    type="is-danger"
                    icon-left="close"
                    outlined
                    @click="datetime = null" />
            </template>
        </b-datetimepicker>
    </b-field>
            <b-form-group label="Book Id">
              <b-form-input type="text" v-model="booklog.BookId" :class="{ 'is-invalid': validation.BookId }"
                placeholder="enter Book Id">
              </b-form-input>
              <div v-if="validation.BookId" class="mt-2">
                <b-alert show variant="danger">{{ validation.BookId[0] }}</b-alert>
              </div>
            </b-form-group>
             <b-form-group label="Member Id">
              <b-form-input type="text" v-model="booklog.MemberId" :class="{ 'is-invalid': validation.MemberId }"
                placeholder="Enter Member Id">
              </b-form-input>
              <div v-if="validation.MemberId" class="mt-2">
                <b-alert show variant="danger">{{ validation.MemberId[0] }}</b-alert>
              </div>
            </b-form-group>
            <b-dropdown disabled aria-role="list">
            <template #trigger>
                <b-button
                    label="Disabled"
                    icon-right="menu-down"
                    v-model="booklog.Status" />
            </template>


            <b-dropdown-item aria-role="listitem">alerted</b-dropdown-item>
            <b-dropdown-item aria-role="listitem">on process</b-dropdown-item>
            <b-dropdown-item aria-role="listitem">done</b-dropdown-item>
        </b-dropdown>
            
            <b-button type="submit" variant="primary">UPDATE</b-button>
          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  export default {
       name: 'editBooklog',
    data() {
      return {
        booklog: {
          StartTime: '',
          EndTime: '',
          BookId: '',
          MemberId: '',
          Status: '',
        },
        
        validation: []
      }
    },
    mounted() {

      this.$axios.get(`/items/booklog/${this.$route.params.id}`)
        .then(response => {
            this.booklog.StartTime   = response.data.data.StartTime;
            this.booklog.EndTime   = response.data.data.EndTime;
            this.booklog.BookId   = response.data.data.BookId;
            this.booklog.MemberId   = response.data.data.MemberId;
            this.booklog.Status   = response.data.data.Status;
        })
    },
    methods: {
      async update(e) {
        e.preventDefault()
        await this.$axios.put(`/items/booklog/${this.$route.params.id}`, {
          StartTime: this.booklog.StartTime,
          EndTime: this.booklog.EndTime,
          BookId: this.booklog.BookId,
          MemberId: this.booklog.MemberId,
          Status: this.booklog.Status,
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


