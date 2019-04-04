<template>
  <div class="container">
    <div class="row">
      <app-contacts-list :contacts="contacts"></app-contacts-list>
      <app-contact-view v-if="!isEditing" :contact="currentContact"></app-contact-view>
      <app-contact-edit v-else :contact="currentContact"></app-contact-edit>

    </div>
  </div>
</template>

<script>

import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

import contacts from './data/contacts.js'
import ContactsList from './ContactsList.vue'
import ContactView from './ContactView.vue'
import ContactEdit from './ContactEdit.vue'

Vue.use(BootstrapVue);

import { eventBus } from './main.js'

export default {
  name: 'app',
  data () {
    return {
      contacts: [],
      currentContactGuid: "5c24597c6a0cc",
      isEditing: false
    }
  },
  created() {
    let self = this;

    //*/
    Vue.axios.get('/contact_list/contacts').then((response) => {
      this.contacts = response.data.contacts;
      this.currentContactGuid = response.data.first_guid;
    });
    //*/

    eventBus.$on('changeContact', function(data) {
      console.log("data: ", data);
      self.isEditing = false
      self.currentContactGuid = data.guid
    })

    eventBus.$on('viewEditContact', function(data) {
      self.isEditing = true;
    })

    eventBus.$on('saveUpdateContact', function(data) {
      let tempContact = self.currentContact
      tempContact.first_name = data.editedContact.first_name
      tempContact.last_name = data.editedContact.last_name
      tempContact.email = data.editedContact.email
      tempContact.home_phone = data.editedContact.home_phone
      tempContact.cell_phone = data.editedContact.cell_phone
      tempContact.address = data.editedContact.address
      tempContact.twitter_handle = data.editedContact.twitter_handle
      tempContact.facebook_handle = data.editedContact.facebook_handle
      tempContact.instagram_handle = data.editedContact.instagram_handle

      let selectedIndex = null;
      self.contacts.map(function(contact, index) {
        if (contact.guid === tempContact.guid) {
          selectedIndex = index;
        }
      })

      Vue.axios.patch('/contact_list/put/' + tempContact.id, tempContact).then((response) => {
        console.log("response.data: ", response.data)
      });

      self.contacts[selectedIndex] = tempContact;
    })
  },
  computed: {
    currentContact() {
      let self = this;
      let selectedIndex = null;
      this.contacts.map(function(contact, index) {
        if (contact.guid === self.currentContactGuid) {
          selectedIndex = index;
        }
      });
      return this.contacts[selectedIndex];
    }
  },
  components: {
    appContactsList: ContactsList,
    appContactView: ContactView,
    appContactEdit: ContactEdit
  }
}
</script>

<style>
  .container {
    margin-top: 25px;
  }

</style>

