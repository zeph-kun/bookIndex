<template>
  <div id="app">
    <Navbar />
    <div class="content-center">
      <h1>Google API Books</h1>
      <form @submit.prevent="search">
        <input v-model="keyword" type="text" class="input" placeholder="Search" required>
        <input type="submit" value="Search" class="button">
      </form>
      <div class="grid grid-cols-3 gap-3">
        <BookList v-for="book in books" :key="book.id" :book="book" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Navbar from '~/components/Navbar.vue'
import BookList from '~/components/BookList.vue'
export default {
  data () {
    return {
      name: 'IndexPage',
      books: [],
      keyword: ''
    }
  },
  methods: {
    async search () {
      const response = await axios.get(`https://www.googleapis.com/books/v1/volumes?q=${this.keyword}?projection=full`)
      console.log(response.data)
      this.books = response.data.items
    }
  },
  components: { Navbar, BookList }
}
</script>
