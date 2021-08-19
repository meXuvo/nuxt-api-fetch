<template>
  <div>
    <nav>
      <ul class="pagination justify-content-center">
        <li
          class="page-item"
          :class="{ disabled: pagination.current_page <= 1 }"
        >
          <a class="page-link" @click.prevent="changePage(1)">First page</a>
        </li>
        <li
          class="page-item"
          :class="{ disabled: pagination.current_page <= 1 }"
        >
          <a
            class="page-link"
            @click.prevent="changePage(pagination.current_page - 1)"
            >Previous</a
          >
        </li>

        <li
          v-for="page in pages"
          :key="page"
          class="page-item"
          :class="isCurrentPage(page) ? 'active' : ''"
        >
          <a class="page-link" @click.prevent="changePage(page)"
            >{{ page }}
            <span v-if="isCurrentPage(page)" class="sr-only">(current)</span>
          </a>
        </li>

        <li
          class="page-item"
          :class="{ disabled: pagination.current_page >= pagination.last_page }"
        >
          <a
            class="page-link"
            @click.prevent="changePage(pagination.current_page + 1)"
            >Next</a
          >
        </li>
        <li
          class="page-item"
          :class="{ disabled: pagination.current_page >= pagination.last_page }"
        >
          <a class="page-link" @click.prevent="changePage(pagination.last_page)"
            >Last page</a
          >
        </li>
      </ul>
    </nav>
    <div>
      <nav
        class="bg-white relative z-0 inline-flex rounded-md shadow-sm -space-x-px"
        aria-label="Pagination"
      >
        <a
          class="relative inline-flex items-center px-2 py-2 rounded-l-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
          @click.prevent="changePage(pagination.current_page - 1)"
        >
          <span class="sr-only">Previous</span>

          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 text-gray-300"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
              clip-rule="evenodd"
            />
          </svg>
        </a>
        <!-- Current: "z-10 bg-indigo-50 border-indigo-500 text-indigo-600", Default: "bg-white border-gray-300 text-gray-500 hover:bg-gray-50" -->
        <a
          href="#"
          aria-current="page"
          class="z-10 bg-indigo-50 border-indigo-500 text-indigo-600 relative inline-flex items-center px-4 py-2 border text-sm font-medium"
        >
          1
        </a>
        <a
          href="#"
          class="bg-white border-gray-300 text-gray-500 hover:bg-gray-50 relative inline-flex items-center px-4 py-2 border text-sm font-medium"
        >
          2
        </a>
        <a
          href="#"
          class="bg-white border-gray-300 text-gray-500 hover:bg-gray-50 hidden md:inline-flex relative items-center px-4 py-2 border text-sm font-medium"
        >
          3
        </a>
        <span
          class="relative inline-flex items-center px-4 py-2 border border-gray-300 bg-white text-sm font-medium text-gray-700"
        >
          ...
        </span>
        <a
          href="#"
          class="bg-white border-gray-300 text-gray-500 hover:bg-gray-50 hidden md:inline-flex relative items-center px-4 py-2 border text-sm font-medium"
        >
          8
        </a>
        <a
          href="#"
          class="bg-white border-gray-300 text-gray-500 hover:bg-gray-50 relative inline-flex items-center px-4 py-2 border text-sm font-medium"
        >
          9
        </a>
        <a
          href="#"
          class="bg-white border-gray-300 text-gray-500 hover:bg-gray-50 relative inline-flex items-center px-4 py-2 border text-sm font-medium"
        >
          10
        </a>
        <a
          class="relative inline-flex items-center px-2 py-2 rounded-r-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
          @click.prevent="changePage(pagination.current_page + 1)"
        >
          <span class="sr-only">Next</span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 text-gray-300"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
            />
          </svg>
        </a>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    paginations: {
      type: Object,
      required: true,
    },
    offset: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      pagination: this.paginations,
    }
  },
  computed: {
    pages() {
      const pages = []

      let from = this.pagination.current_page - Math.floor(this.offset / 2)

      if (from < 1) {
        from = 1
      }

      let to = from + this.offset - 1
      if (to > this.pagination.last_page) {
        to = this.pagination.last_page
      }

      while (from <= to) {
        pages.push(from)
        from++
      }

      return pages
    },
  },
  methods: {
    isCurrentPage(page) {
      return this.pagination.current_page === page
    },
    changePage(page) {
      if (page > this.pagination.last_page) {
        console.log(page)
        console.log(this.pagination.last_page)
        page = this.pagination.last_page
      }
      this.pagination.current_page = page
      this.$emit('paginate', page)
    },
  },
}
</script>

<style scoped></style>
