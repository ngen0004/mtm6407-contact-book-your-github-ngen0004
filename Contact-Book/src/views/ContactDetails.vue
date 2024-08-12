<template>
    <div v-if="contact" class="contact-details">
        <header class="header">
            <router-link to="/" class="back-link">&lt; Contacts</router-link>
            <router-link :to="'/edit/' + contact.id" class="edit-link">Edit</router-link>
        </header>
      <h2>{{ contact.firstName }} {{ contact.lastName }}</h2>
      <div class="contact-info">
        <div class="info-item">
            <p><strong>Email:</strong> {{ contact.email }}</p>
        </div>
      </div>      
      <button @click="deleteContact" class="delete">Delete</button>
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

<style>
.contact-details {
    max-width: 400px;
    margin: 100px auto;
    padding: 120px;
    font-family: Arial, sans-serif;
    background-color: #eae5e5;
    box-shadow: 0px 4px 6px rgba(12, 12, 12, 0.354);
    border-radius: 8px;
    text-align: left;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.back-link, .edit-link {
  font-size: 14px;
  text-decoration: none;
  color: #007bfe;
}

.back-link:hover, .edit-link:hover {
  color: #77e410;
}

h2 {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 15px;
}

.contact-info {
  border-top: 1px solid #c7c7c7;
  padding-top: 20px;
}

.info-item {
  margin-bottom: 15px;
}

.info-item p {
  display: block;
  margin-bottom: 5px;
  font-size: 14px;
  color: #6169f7;
}
.info-item strong {
  color: black;
}
.delete {
    background-color: #ff0000;
    color: rgb(252, 252, 252);
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    font-size: 15px;
    cursor: pointer;
    margin-top: 10px;
    font-weight: bold;
}
.delete:hover {
    background-color: #bbd462;
    color: #000;
}

</style>