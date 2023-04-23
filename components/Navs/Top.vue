<template>
  <div ref="topElement" class="topElement">
    <NuxtLink to="/">homepage</NuxtLink>
    <NuxtLink :to="'/nasa'" >Nasa</NuxtLink>
    <NuxtLink :to="'/cars/' + name" >car</NuxtLink>
  </div>
</template>

<script>
export default {
  name: "Top",
  data() {
    return {
      name: '123'
    }
  }
}
</script>

<style scoped>
.topElement {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: royalblue;
  color: white;
  border-bottom: 5px solid black;
  min-height: 50px;
}

a {
  color: white;
  font-size: 16px;
  padding: 0 10px;
  text-decoration: none;
  text-transform: uppercase;
}

.nuxt-link-exact-active,a:hover {
  color: yellow;
}

</style>
