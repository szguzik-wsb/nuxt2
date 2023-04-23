<template>
  <div>
    <h1>Opis portalu o samochodach wojskowych</h1>
  </div>
</template>

<script>
export default {
  name: "about",
  head() {
    return {
      title: 'Opis portalu o samochodach wojskowych', // ustawiamy title dla strony
      meta: [
        {
          hid: 'description', // unikalny identyfikator (ukryty)
          name: 'description', // nazwa atrybutu tagu meta,
          content: 'Opis portalu o samochodach wojskowych' // opis tagu
        }
      ]
    }
  }
}
</script>

<style scoped>

</style>
