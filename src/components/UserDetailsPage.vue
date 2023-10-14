<script setup>
import {ref, computed, watch} from 'vue';
const user = ref({
  name: 'John Doe',
  profileImage: 'https://dummyimage.com/50x50/000/fff',
  birthdate: '2000-01-01',
  email: '',
  description: 'A user description.'
});

const birthYear = computed(() => {
  return new Date(user.value.birthdate).getFullYear();
});

const canVoteMessage = computed(() => {
  const birthYear = new Date(user.value.birthdate).getFullYear();
  const currentYear = new Date().getFullYear();
  const age = currentYear - birthYear;
  return age >= 18 ? 'Yes' : 'No';
});

watch(user, (birthYear, age) => {
  console.log('User changed:', birthYear, age);
});

const saveUser = () => {
  // You can add logic to save user data to the server or perform any necessary actions here.
  // For this example, we'll simply log the user data.
  console.log('User data saved:', user.value);
};

</script>

<template>
  <div id="UserDetails" >
    <h2>User Details</h2>
    <br>

    <form @submit.prevent="saveUser" class="border-b border-gray-900/10 pb-12">

      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="user.name">
      </div>
      <div>
        <label for="profileImage">Profile Image URL:</label>
        <input type="text" id="profileImage" v-model="user.profileImage">
      </div>
      <div>
        <label for="birthdate">Birthdate:</label>
        <input type="date" id="birthdate" v-model="user.birthdate">
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="user.email">
      </div>
      <div>
        <label for="description">Description:</label>
        <textarea id="description" v-model="user.description"></textarea>
      </div>

      <p><strong>Birth Year:</strong> {{ birthYear }}</p>
      <p><strong>Legal Voting Age:</strong> {{ canVoteMessage }}</p>

      <button id="savebutton" type="submit">Save</button>
    </form>
    <br>
    <br>

    <div class="preview">
      <h2>Preview</h2>
      <p><strong>Name:</strong> {{ user.name }}</p>
      <img :src="user.profileImage" alt="Profile Image" style="max-width: 200px;">
      <p><strong>Birthdate:</strong> {{ user.birthdate }}</p>
      <p><strong>Birth Year:</strong> {{ birthYear }}</p>
      <p><strong>Email:</strong> {{ user.email }}</p>
      <p><strong>Description:</strong> {{ user.description }}</p>
      <p><strong>Legal Voting Age:</strong> {{ canVoteMessage }}</p>

    </div>
  </div>

</template>

<style scoped>
#UserDetails {
  max-width: 1040px;
  margin: 0 auto;
  background-color: #ccc;
  color: fff ;
  padding: 1rem;
  
}

.preview {
  border: 1px solid #ccc;
  padding: 1rem;
  margin-top: 1rem;
  background: #fff;
  color: #000;


}
#savebutton {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;

}


</style>




