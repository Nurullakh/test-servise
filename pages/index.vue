<template>
  <div class="main-page">
    <CreateSurvey :success="success" @submit="submit" />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      success: false,
    }
  },
  methods: {
    submit(data) {
      // отправка на сервер
      this.success = true
      this.$nextTick(() => {
        this.success = false
      })
    },
  },
}
</script>

