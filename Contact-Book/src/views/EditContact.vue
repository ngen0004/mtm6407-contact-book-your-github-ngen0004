<template>
    <div v-if="contact" class="edit-contact">
        <header class="header">
            <router-link to="/" class="back-link">&lt; Contacts</router-link>
        </header>
        <h2>Edit Contact</h2>
        <form @submit.prevent="editContact">
            <div class="input-group">
                <input v-model="contact.firstName" placeholder="First Name" required />
                <input v-model="contact.lastName" placeholder="Last Name" required />
            </div>
            <div class="input-group">
                <input v-model="contact.email" type="email" placeholder="Email" required />
            </div>
            <div class="input-group">
                <button type="submit" class="save-button">Update Contact</button>
                <router-link to="/" class="cancel-link">Cancel</router-link>
            </div>     
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

<style>
.edit-contact {
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
    margin-bottom: 20px;
}

.back-link {
    font-size: 14px;
    text-decoration: none;
    color: #007bff;
}

.back-link:hover {
    color: #0056b3;
}

h2 {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
}

.contact-form {
    border: 1px solid #e0e0e0;
    padding: 20px;
    border-radius: 5px;
    background-color: #f9f9f9;
}

.input-group {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
}

.input-group input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.button-group {
    display: flex;
    gap: 20px;
    align-items: center;
}

.save-button {
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
}

.save-button:hover {
    background-color: #253241;
}

.cancel-link {
    font-size: 16px;
    padding: 10px 20px;
    background-color: #ff1500;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.cancel-link:hover {
    background-color: #8eb82d;
}

</style>