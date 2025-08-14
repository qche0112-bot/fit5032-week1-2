<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-8 offset-md-2">

        <h1 class="text-center mb-4" style="text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.5);">
          用户信息表单 / 凭证
        </h1>

        <form @submit.prevent="submitForm">

          <div class="mb-3">
            <label for="username" class="form-label">用户名：</label>
            <input type="text" id="username" class="form-control" v-model="formData.username" required />
          </div>

          <div class="mb-3">
            <label for="password" class="form-label">密码：</label>
            <input type="password" id="password" class="form-control" v-model="formData.password" required />
          </div>

          <div class="form-check mb-3">
            <input type="checkbox" id="isAustralian" class="form-check-input" v-model="formData.isAustralian" />
            <label for="isAustralian" class="form-check-label">澳大利亚居民？</label>
          </div>

          <div class="mb-3">
            <label for="reason" class="form-label">加入原因：</label>
            <textarea id="reason" class="form-control" rows="3" v-model="formData.reason"></textarea>
          </div>

          <div class="mb-3">
            <label for="gender" class="form-label">性别：</label>
            <select id="gender" class="form-select" v-model="formData.gender" required>
              <option value="" disabled selected>请选择</option>
              <option value="female">女</option>
              <option value="male">男</option>
              <option value="other">其他</option>
            </select>
          </div>

          <button type="submit" class="btn btn-primary me-2">提交</button>
          <button type="button" class="btn btn-secondary" @click="clearForm">清空</button>
        </form>

        <div class="row mt-5" v-if="submittedCards.length">
          <div class="d-flex flex-wrap justify-content-start">
            <div v-for="(card, index) in submittedCards" :key="index" class="card m-2" style="width: 18rem;">
              <div class="card-header text-white bg-primary">
                用户信息
              </div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">用户名: {{ card.username }}</li>
                <li class="list-group-item">密码: {{ card.password }}</li>
                <li class="list-group-item">澳大利亚居民: {{ card.isAustralian ? '是' : '否' }}</li>
                <li class="list-group-item">性别: {{ card.gender }}</li>
                <li class="list-group-item">加入原因: {{ card.reason }}</li>
              </ul>
            </div>
          </div>
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
  // 深拷贝当前表单数据，避免后续修改影响已提交数据
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
/* 额外卡片样式 */
.card {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>