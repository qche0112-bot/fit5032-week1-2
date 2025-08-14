<script setup>
import { ref, computed } from 'vue'

const authors = ref([
  { id: 1, name: 'Jane Austen', birthYear: 1775, famousWorks: [{ title: 'Pride and Prejudice' }, { title: 'Sense and Sensibility' }] },
  { id: 2, name: 'George Orwell', birthYear: 1903, famousWorks: [{ title: '1984' }, { title: 'Animal Farm' }] },
  { id: 3, name: 'Agatha Christie', birthYear: 1890, famousWorks: [{ title: 'Murder on the Orient Express' }, { title: 'Death on the Nile' }] },
])

const modernAuthors = computed(() =>
  authors.value.filter(author => author.birthYear > 1850)
)

const allFamousWorks = computed(() =>
  authors.value.flatMap(author => author.famousWorks.map(work => work.title))
)

const showMessage = ref(false)
</script>

<template>
  <div>
    <button @click="showMessage = !showMessage">Toggle Message</button>

    <p v-if="showMessage" class="message success">
      ✨ You're a Vue superstar! ✨
    </p>
    <p v-else class="message">
      Click the button to see a message.
    </p>

    <h2>Iterating through Arrays</h2>
    <ul>
      <li v-for="author in authors" :key="author.id">
        {{ author.name }} ({{ author.birthYear }})
      </li>
    </ul>

    <h2>Filtering Arrays</h2>
    <p>Authors born after 1850:</p>
    <ul>
      <li v-for="author in modernAuthors" :key="author.id">
        {{ author.name }} ({{ author.birthYear }})
      </li>
    </ul>

    <h2>Mapping Arrays</h2>
    <p>Famous works:</p>
    <ul>
      <li v-for="work in allFamousWorks" :key="work">
        {{ work }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
li {
  background-color: #eee;
  padding: 0.5rem 1rem;
  margin-bottom: 0.5rem;
  border-radius: 4px;
}
h2 {
  margin-top: 2rem;
  color: #333;
}
.message {
  margin: 1rem 0;
  font-size: 1.2rem;
}
.success {
  color: green;
}
</style>



