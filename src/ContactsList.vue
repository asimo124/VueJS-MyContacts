<template>
  <div class="col-md-4">
    <ul class="contact-list">
      <li v-for="contact in contacts" @click.prevent="selectContact(contact.guid)">
        <a href="#" >{{ contact.first_name }} {{contact.last_name}}</a></li>
    </ul>
  </div>
</template>

<script>

  import { eventBus } from './main.js';

  export default {
    props: {
      contacts: {
        type: Array,
        required: true
      }
    },
    methods: {
      selectContact(selectedGuid) {
        window.scrollTo(0,0);
        eventBus.$emit('changeContact', {
          guid: selectedGuid
        });
      }
    }

  }
</script>

<style>

  ul.contact-list {
    padding-top: 1px;
    padding-bottom: 1px;
    background-color: #512DA8;
    padding-inline-start: 0px;
    border-radius: 5px;
    background-color: #6200EE;
  }

  ul.contact-list li {
    font-size: 16px;
    font-weight: bold;
    /*color: #311B92;*/
    list-style-type: none;
    /*background-color: white;*/
    padding: 15px 10px;
    /*border-radius: 5px;*/
    margin-top: 5px;
    margin-bottom: 5px;
    padding-left: 20px;
    /*margin-right: 5px;
    margin-left: 5px;*/
    border-bottom: 1px solid white;
  }

  ul.contact-list li a:hover, ul.contact-list li a:visited, ul.contact-list li a:link, ul.contact-list li a:active  {
    color: white;
    text-decoration: none;
  }

</style>
