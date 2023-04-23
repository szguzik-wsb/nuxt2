<template>
<div class="container center">
  <h1>Nasa - {{ currentCollection }}</h1>
  <input placeholder="Search.." v-model="findString">
  <button @click="fetchData(findString)">Znajdz</button>


  <div class="loader" v-if="loader">
    <svg xmlns="http://www.w3.org/2000/svg" width="75" height="27" viewBox="0 0 75 27">
      <g fill-rule="evenodd">
        <polygon points="6.1 14.9 7.7 19.4 12.3 19.5 8.5 22.2 10 26.7 6.1 24 2.3 26.7 3.7 22.2 0 19.5 4.6 19.4"/>
        <polygon points="20.4 4.1 21.8 8.5 26.6 8.5 22.8 11.4 24.3 15.8 20.4 13.1 16.6 15.8 18 11.4 14.3 8.5 18.9 8.5"/>
        <polygon points="37.9 0 39.3 4.5 44 4.5 40.2 7.3 41.6 11.8 37.9 9 34 11.8 35.4 7.3 31.7 4.5 36.3 4.5"/>
        <polygon points="54.9 4.1 56.3 8.5 61 8.5 57.2 11.4 58.6 15.8 54.9 13.1 51 15.8 52.4 11.4 48.6 8.5 53.4 8.5"/>
        <polygon points="68.9 15.2 70.3 19.7 75 19.8 71.2 22.5 72.7 27 68.9 24.3 65 27 66.4 22.5 62.7 19.8 67.3 19.7"/>
      </g>
    </svg>
  </div>


  <div style="display: flex; flex-wrap: wrap; width: 100%; justify-content: center" v-else>
    <template v-for="value in dataArr">

      <template v-for="(link, index) in value.links">
        <img
          @click="setModal(link.href)"
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
      loader: false,
      dataArr: [],
      findString:"",
      currentCollection: ""
    }
  },

  methods: {

  setModal(value) {
    const data = {
      state: true,
      content: value
    }
    this.$nuxt.$emit('runModal', data);
  },

  async fetchData(value) {
    this.loader = true;
    await axios.get('https://images-api.nasa.gov/search?q=' + value)
      .then(res => {
        console.log(res.data.collection.items)
        this.dataArr = res.data.collection.items;
        this.loader = false;
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

img {
  cursor: pointer;
  border: 2px solid white;
}

img:hover {
  border: 2px solid #0d60ec;
}

button{
  border: 1px solid royalblue;
  padding: 5px 10px;
  margin: 2px;
  background-color: royalblue;
  color: white;
  text-transform: uppercase;
  cursor: pointer;
}

button:hover {
  background-color: white;
  color: royalblue;
}

input {
  margin: 5px;
  padding: 6px 25px;
  text-transform: uppercase;
}


loader svg {
  width: 300px;
  height: 108px;
}
.loader svg polygon {
  fill: #ccc;
  color: #ccc;
  animation: change 2.4s infinite;
}
.loader svg polygon:nth-child(1) {
  animation-delay: 0.4s;
}
.loader svg polygon:nth-child(2) {
  animation-delay: 0.8s;
}
.loader svg polygon:nth-child(3) {
  animation-delay: 1.2s;
}
.loader svg polygon:nth-child(4) {
  animation-delay: 1.6s;
}
.loader svg polygon:nth-child(5) {
  animation-delay: 2s;
}
@keyframes change {
  0% {
    fill: #ccc;
    color: #ccc;
  }
  30% {
    fill: #da3d18;
    color: #da3d18;
  }
  100% {
    fill: #ccc;
    color: #ccc;
  }
}
</style>
