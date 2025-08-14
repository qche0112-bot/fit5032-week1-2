<script setup>
import { ref, computed } from 'vue'

const authors = ref([
  {
    name: 'Mark Twain',
    birthYear: 1835,
    famousWorks: [
      { title: 'Adventures of Huckleberry Finn' },
      { title: 'The Adventures of Tom Sawyer' }
    ]
  },
  {
    name: 'Virginia Woolf',
    birthYear: 1882,
    famousWorks: [
      { title: 'Mrs Dalloway' },
      { title: 'To the Lighthouse' }
    ]
  },
  {
    name: 'George Orwell',
    birthYear: 1903,
    famousWorks: [
      { title: '1984' },
      { title: 'Animal Farm' }
    ]
  },
  {
    name: 'Jane Austen',
    birthYear: 1775,
    famousWorks: [
      { title: 'Pride and Prejudice' },
      { title: 'Sense and Sensibility' }
    ]
  }
])

const modernAuthors = computed(() =>
  authors.value.filter(author => author.birthYear > 1850)
)

const allFamousWorks = computed(() =>
  authors.value.flatMap(author => author.famousWorks.map(work => work.title))
)
</script>

<template>
  <div>
    <h2>birthday>1850</h2>
    <ul>
      <li v-for="author in modernAuthors" :key="author.name">
        {{ author.name }} ({{ author.birthYear }})
      </li>
    </ul>

    <h2>all famous tital</h2>
    <ul>
      <li v-for="(title, index) in allFamousWorks" :key="index">
        {{ title }}
      </li>
    </ul>
  </div>
</template>