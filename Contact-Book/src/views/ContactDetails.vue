<template>
    <div v-if="contact">
      <h2>{{ contact.firstName }} {{ contact.lastName }}</h2>
      <p>Email: {{ contact.email }}</p>
      <router-link :to="'/edit/' + contact.id">Edit</router-link>
      <button @click="deleteContact">Delete</button>
      <router-link to="/">Back to Contacts</router-link>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        contact: null,
      };
    },
    mounted() {
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      this.contact = contacts.find(contact => contact.id === parseInt(this.$route.params.id));
    },
    methods: {
      deleteContact() {
        const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
        const updatedContacts = contacts.filter(contact => contact.id !== parseInt(this.$route.params.id));
        localStorage.setItem('contacts', JSON.stringify(updatedContacts));
        this.$router.push('/');
      },
    },
  };
  </script>
  