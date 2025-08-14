<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-12 text-center">
        <h1 style="white-space: nowrap; text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.5);">
          User information form/credential
        </h1>
      </div>
    </div>

    <div class="row mt-4">
      <div class="col-md-4 text-center d-flex align-items-center justify-content-center">
        <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg"
             alt="Vue Logo" style="max-width: 150px;">
      </div>

      <div class="col-md-8">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label for="username" class="form-label">username：</label>
            <input type="text" id="username" class="form-control" v-model="formData.username" required />
          </div>

          <div class="mb-3">
            <label for="password" class="form-label">password：</label>
            <input type="password" id="password" class="form-control" v-model="formData.password" required />
          </div>

          <div class="form-check mb-3">
            <input type="checkbox" id="isAustralian" class="form-check-input" v-model="formData.isAustralian" />
            <label for="isAustralian" class="form-check-label">Australian residents？</label>
          </div>

          <div class="mb-3">
            <label for="reason" class="form-label">Reasons for joining：</label>
            <textarea id="reason" class="form-control" rows="3" v-model="formData.reason"></textarea>
          </div>

          <div class="mb-3">
            <label for="gender" class="form-label">Sex：</label>
            <select id="gender" class="form-select" v-model="formData.gender" required>
              <option value="" disabled selected>please selected</option>
              <option value="female">female</option>
              <option value="male">male</option>
              <option value="other">other</option>
            </select>
          </div>

          <button type="submit" class="btn btn-primary me-2">submit</button>
          <button type="button" class="btn btn-secondary" @click="clearForm">cleaning</button>
        </form>
      </div>
    </div>

    <div class="row mt-5" v-if="submittedCards.length">
      <div class="d-flex flex-wrap justify-content-start">
        <div v-for="(card, index) in submittedCards" :key="index" class="card m-2" style="width: 18rem;">
          <div class="card-header text-white bg-primary">
            User information
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">Username: {{ card.username }}</li>
            <li class="list-group-item">Password: {{ card.password }}</li>
            <li class="list-group-item">Australian residents？: {{ card.isAustralian ? 'yes' : 'no' }}</li>
            <li class="list-group-item">Sex: {{ card.gender }}</li>
            <li class="list-group-item">Reasons for joining: {{ card.reason }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({
  username: '',
  password: '',
  isAustralian: false,
  reason: '',
  gender: ''
})

const submittedCards = ref([])

function submitForm() {
  submittedCards.value.push({ ...formData.value })
  clearForm()
}

function clearForm() {
  formData.value = {
    username: '',
    password: '',
    isAustralian: false,
    reason: '',
    gender: ''
  }
}
</script>

<style scoped>
.card {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>
