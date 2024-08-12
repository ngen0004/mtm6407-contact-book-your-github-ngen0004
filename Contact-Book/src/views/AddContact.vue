<template>
    <div>
      <h2>Add New Contact</h2>
      <form @submit.prevent="addContact">
        <input v-model="firstName" placeholder="First Name" required />
        <input v-model="lastName" placeholder="Last Name" required />
        <input v-model="email" type="email" placeholder="Email" required />
        <button type="submit">Add</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        firstName: '',
        lastName: '',
        email: '',
      };
    },
    methods: {
      addContact() {
        const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
        const newContact = {
          id: Date.now(),
          firstName: this.firstName,
          lastName: this.lastName,
          email: this.email,
        };
        contacts.push(newContact);
        localStorage.setItem('contacts', JSON.stringify(contacts));
        this.$router.push(`/contact/${newContact.id}`);
      },
    },
  };
  </script>
  