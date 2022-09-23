<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg text-center">
    <img class="w-min mx-auto" :src="info.imageLinks.smallThumbnail" :alt="info.title">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{ info.title }}</div>
        <p class="text-gray-700 text-base">
          <span v-if="!info.description">No description</span>
          <span v-else>
            {{ info.description.slice(0, 200) + '...'}}
          </span>
        </p>
    </div>
    <div class="px-6 pt-4 pb-2">
      <span v-if="!info.authors">No authors to display</span>
      <span v-else>
        <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{{ info.authors.toString() }}</span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    book: {
      type: Object,
      required: true
    }
  },
  computed: {
    info () {
      return this.book.volumeInfo
    }
  }
}
</script>
