<template>
    <div class="contact-book">
        <header class="header">
            <h1>Contact Book</h1>
            <router-link to="/add" class="add-button1">+</router-link>
        </header>
      <input v-model="search" placeholder="Search contacts" class="search-input" />
      <ul class="contact-list">
        <li v-for="contact in filteredContacts" :key="contact.id" class="contact-item">
          <router-link :to="'/contact/' + contact.id" class="contact-link">
            {{ contact.firstName }} {{ contact.lastName }}
          </router-link>
        </li>
      </ul>
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
  
<style>
    .contact-book {
        max-width: 400px;
        margin: 100px auto;
        padding: 120px;
        font-family: Arial, sans-serif;
        background-color: #eae5e5;
        box-shadow: 0px 4px 6px rgba(12, 12, 12, 0.575);
        border-radius: 8px;
        text-align: left;
    }

    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }

    .header h1 {
        font-size: 24px;
        font-weight: bold;
        margin: 0;
    }

    .add-button1 {
        font-size: 30px;
        text-decoration: none;
        color: #0037ff;
    }

    .add-button1:hover {
        color: #77e410;
    }

    .search-input {
        width: 100%;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        padding: 10px;
    }

    .contact-list {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .contact-item {
        margin-bottom: 10px;
    }

    .contact-link {
        display: block;
        padding: 15px;
        background-color: #f8f8f8;
        border-radius: 5px;
        text-decoration: none;
        color: #333;
        font-size: 18px;
        transition: background-color 0.3s;
    }

    .contact-link:hover {
        background-color: #a8a8a8;
    }
</style>