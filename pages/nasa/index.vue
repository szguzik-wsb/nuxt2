<template>
<div class="container center">
  <h1>Nasa - {{ currentCollection }}</h1>
  <input placeholder="Search.." v-model="findString">
  <button @click="fetchData(findString)">Znajdz</button>
  <div style="display: flex; flex-wrap: wrap; width: 100%; justify-content: center">
    <template v-for="value in dataArr">

      <template v-for="(link, index) in value.links">
        <img
          alt=""
          v-if="index === 0"
          :data-index="index"
          :src="link.href"
          style="width: 100px; height: 100px; object-fit: cover; padding: 5px"/>
      </template>

    </template>
  </div>

</div>
</template>

<script>
import axios from "axios";
export default {
  name: "index",

  created() {
    this.fetchData("sun")
  },

  data() {
    return {
      dataArr: [],
      findString:"",
      currentCollection: ""
    }
  },

  methods: {
  async fetchData(value) {
    await axios.get('https://images-api.nasa.gov/search?q=' + value)
      .then(res => {
        console.log(res.data.collection.items)
        this.dataArr = res.data.collection.items;
        this.currentCollection = value;
        this.findString = "";
      })
      .catch(error => {
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>
.center {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
