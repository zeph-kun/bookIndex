<template>
  <div id="app">
    <Navbar />
    <div class="container mx-auto">
      <div class="flex items-center flex-col">
        <h1>Google API Books</h1>
        <form @submit.prevent="search">
          <div>
            <input v-model="keyword" type="text" class="block mb-2 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-80 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Search" required>
          </div>
          <div>
            <input type="submit" value="Search" class="block mb-2 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
          </div>
        </form>
      </div>
    </div>
    <div class="grid grid-cols-3 gap-3">
      <BookList v-for="book in books" :key="book.id" :book="book" />
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
