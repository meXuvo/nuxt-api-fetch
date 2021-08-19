<template>
  <div>
    <div v-for="(data, index) in loadDatas" :key="index">
      <p>{{ data.title }}</p>
    </div>
    <button type="button" @click="fetchMoreData">next</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loadDatas: null,
      storeResponse: null,
    }
  },
  created() {
    this.searchResults()
  },
  methods: {
    async searchResults() {
      await this.$axios
        .$get('https://api.spiro.study/search?limit=1&q=java&type=videos')
        .then((res) => {
          this.storeResponse = res
          this.loadDatas = res.results
        })
    },
    async fetchMoreData() {
      await this.$axios.$get(this.storeResponse.next).then((res) => {
        this.loadDatas.push(res.results)
      })
    },
  },
}
</script>

<style></style>
