<template>
    <div v-if="contact">
      <h2>Edit Contact</h2>
      <form @submit.prevent="editContact">
        <input v-model="contact.firstName" placeholder="First Name" required />
        <input v-model="contact.lastName" placeholder="Last Name" required />
        <input v-model="contact.email" type="email" placeholder="Email" required />
        <button type="submit">Save</button>
      </form>
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
      editContact() {
        const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
        const index = contacts.findIndex(contact => contact.id === parseInt(this.contact.id));
        contacts[index] = this.contact;
        localStorage.setItem('contacts', JSON.stringify(contacts));
        this.$router.push(`/contact/${this.contact.id}`);
      },
    },
  };
  </script>
  