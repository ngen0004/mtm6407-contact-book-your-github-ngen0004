<template>
    <div>
      <h1>Contact Book</h1>
      <input v-model="search" placeholder="Search contacts" />
      <ul>
        <li v-for="contact in filteredContacts" :key="contact.id">
          <router-link :to="'/contact/' + contact.id">
            {{ contact.lastName }}, {{ contact.firstName }}
          </router-link>
        </li>
      </ul>
      <router-link to="/add">Add New Contact</router-link>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        search: '',
        contacts: JSON.parse(localStorage.getItem('contacts')) || [],
      };
    },
    computed: {
      filteredContacts() {
        return this.contacts
          .filter(
            (contact) =>
              contact.firstName.toLowerCase().includes(this.search.toLowerCase()) ||
              contact.lastName.toLowerCase().includes(this.search.toLowerCase())
          )
          .sort((a, b) => a.lastName.localeCompare(b.lastName));
      },
    },
  };
  </script>
  