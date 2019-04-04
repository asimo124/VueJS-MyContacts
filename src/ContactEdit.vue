<template>
  <div class="col-md-8">
    <div class="image_holder">
      <img :src="contact.profile_pic" width="100%" />
      <h3>{{ contact.first_name }} {{ contact.last_name }}</h3>
      <h4><a :href="'mailto: ' + contact.email" >{{ contact.email }}</a></h4>
      <button class="btn mat-btn-other" @click="submitEditContact()">Save</button>
    </div>
    <div style="clear: both; height: 17px;"></div>
    <div class="alert alert-success" v-if="didSave">You have updated this contact.</div>
    <form @submit.prevent>
      <div class="row">
          <div class="col-md-12 col-xs-12">
            <div class="form-group">
              <label for="first_name" >First Name</label>
              <input type="text" name="first_name" :class="['form-control', {invalid: invalidFields.includes('first_name')}]" v-model="contactToEdit.first_name" />
            </div>
            <div class="form-group">
              <label for="last_name" >Last Name</label>
              <input type="text" name="last_name" :class="['form-control', {invalid: invalidFields.includes('last_name')}]" v-model="contactToEdit.last_name" />
            </div>
            <div class="form-group">
              <label for="email" >Email</label>
              <input type="text" name="email" :class="['form-control', {invalid: invalidFields.includes('email')}]" v-model="contactToEdit.email" />
            </div>
            <div class="form-group">
              <label for="home_phone" >Home Phone</label>
              <input type="text" name="home_phone" :class="['form-control', {invalid: invalidFields.includes('home_phone')}]" v-model="contactToEdit.home_phone" />
            </div>
            <div class="form-group">
              <label for="cell_phone" >Cell Phone</label>
              <input type="text" name="cell_phone" :class="['form-control', {invalid: invalidFields.includes('cell_phone')}]" v-model="contactToEdit.cell_phone" />
            </div>
            <div class="form-group">
              <label for="address" >Address</label>
              <input type="text" name="address" :class="['form-control', {invalid: invalidFields.includes('address')}]" v-model="contactToEdit.address" />
            </div>
            <div class="form-group">
              <label for="twitter_handle" >Twitter</label>
              <input type="text" name="twitter_handle" :class="['form-control', {invalid: invalidFields.includes('twitter_handle')}]" v-model="contactToEdit.twitter_handle" />
            </div>
            <div class="form-group">
              <label for="facebook_handle" >Facebook</label>
              <input type="text" name="twitter_handle" :class="['form-control', {invalid: invalidFields.includes('facebook_handle')}]" v-model="contactToEdit.facebook_handle" />
            </div>
            <div class="form-group">
              <label for="instagram_handle" >Instagram</label>
              <input type="text" name="twitter_handle" :class="['form-control', {invalid: invalidFields.includes('instagram_handle')}]" v-model="contactToEdit.instagram_handle" />
            </div>
          </div>
      </div>
    </form>



  </div>
</template>

<script>

  import {eventBus} from "./main";

  export default {
    data() {
      return {
        invalidFields: [],
        didSave: false,
        contactToEdit: {
          guid: this.contact.guid,
          first_name: this.contact.first_name,
          last_name: this.contact.last_name,
          email: this.contact.email,
          home_phone: this.contact.home_phone,
          cell_phone: this.contact.cell_phone,
          address: this.contact.address,
          twitter_handle: this.contact.twitter_handle,
          facebook_handle: this.contact.facebook_handle,
          instagram_handle: this.contact.instagram_handle,
          profile_pic: this.contact.profile_pic
        }
      }
    },
    props: {
      contact: {
        type: Object,
        required: true
      }
    },
    methods: {
      submitEditContact() {
        this.invalidFields = [];
        this.didSave = false;
        if (!this.contactToEdit.first_name) {
          this.invalidFields.push('first_name')
        }
        if (!this.contactToEdit.last_name) {
          this.invalidFields.push('last_name')
        }
        if (!this.contactToEdit.email) {
          this.invalidFields.push('email')
        }
        if (!this.contactToEdit.home_phone) {
          this.invalidFields.push('home_phone')
        }
        if (!this.contactToEdit.cell_phone) {
          this.invalidFields.push('cell_phone')
        }
        if (!this.contactToEdit.address) {
          this.invalidFields.push('address')
        }
        if (!this.contactToEdit.twitter_handle) {
          this.invalidFields.push('twitter_handle')
        }
        if (!this.contactToEdit.facebook_handle) {
          this.invalidFields.push('facebook_handle')
        }
        if (!this.contactToEdit.instagram_handle) {
          this.invalidFields.push('instagram_handle')
        }
        if (this.invalidFields.length == 0) {
          this.didSave = true



          eventBus.$emit('saveUpdateContact', {
            editedContact: this.contactToEdit
          })
        }
      },
      hasInvalid(fieldName) {
        this.invalidFields.map(function(field, index) {
          if (field == fieldName) {
            return true
          }
        })
        return false
      }
    }
  }
</script>

<style>

  .image_holder {
    width: 42%;
    margin: 0 auto;
    text-align: center;
  }

  .image_holder img {
    margin-bottom: 7px;
    border: 3px solid #3700b3;
    border-radius: 12px;
  }

  .image_holder h4 a:hover, .image_holder h4 a:active, .image_holder h4 a:visited, .image_holder h4 a:link   {
    color: black;
  }

  ul.view_fields_holder {
    margin-top: 27px;
    list-style-type: none;
  }
  ul.view_fields_holder li {
    margin-top: 5px;
    margin-bottom: 5px;
  }

  button.mat-btn-other, button.mat-btn-other:hover {
    background-color: #0d47a1;
    color: #FFF;
  }

  input[type="text"].invalid {
    border: 1px solid red;
  }


</style>
