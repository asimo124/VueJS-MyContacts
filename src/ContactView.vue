<template>
  <div class="col-md-8">
    <div class="image_holder">
      <img :src="contact.profile_pic" width="100%" />
      <h3>{{ contact.first_name }} {{ contact.last_name }}</h3>
      <h4><a :href="'mailto: ' + contact.email" >{{ contact.email }}</a>&nbsp;</h4>
      <button class="btn btn-primary mat-btn" @click.prevent="editContact()">Edit</button>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <ul class="view_fields_holder">
          <li><strong>Home Phone:</strong> {{ contact.home_phone}}</li>
          <li><strong>Cell Phone:</strong> {{ contact.cell_phone}}</li>
          <li><strong>Address:</strong> {{ contact.address}}</li>
          <li><strong>Twitter:</strong> <a :href="'https://twitter.com/' + contact.twitter_handle" >{{ contact.twitter_handle}}</a></li>
          <li><strong>Facebook:</strong> <a :href="'https://facebook.com/' + contact.facebook_handle" >{{ contact.facebook_handle}}</a></li>
          <li><strong>Instagram:</strong> <a :href="'https://instagram.com/' + contact.instagram_handle" >{{ contact.instagram_handle}}</a></li>
        </ul>






      </div>
    </div>


  </div>
</template>

<script>

  import { eventBus } from './main.js';

  export default {
    props: {
      contact: {
        type: Object,
        required: true
      }
    },
    methods: {
      editContact() {
        eventBus.$emit('viewEditContact', {});
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

  button.mat-btn {
    background-color: #1e88e5 ;
  }
</style>
