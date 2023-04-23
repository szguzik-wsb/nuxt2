<template>
  <div>
    <NavsTop/>
    <Nuxt />
    <ModalsBasicModal v-if="modal.show">
      <img :src="modal.content" style="width: 100%; height: 100%">
    </ModalsBasicModal>
  </div>
</template>
<script>
export default {
  name: "NuxtComponent",
  data() {
    return {
        modal: {
          show: false,
          content: null
        }
    }
  },

  created() {
    this.$nuxt.$on('runModal', ($event) => this.setModal($event))
    this.$nuxt.$on('closeModal', ($event) => this.setModal($event))
  },

  methods: {
    setModal(e) {
      this.modal.content = e.content
      this.modal.show = e.state
    }
  }
}
</script>
