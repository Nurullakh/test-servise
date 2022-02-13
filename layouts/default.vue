<template>
  <div class="site-carcass">
    <Aside> </Aside>
    <div class="site-carcass__wrapper">
      <Header />
      <main class="site-carcass__container">
        <div class="site-carcass__content">
          <nuxt />
        </div>
      </main>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DefaultLayout',
}
</script>

<style lang="scss" scoped>
.site-carcass {
  min-height: 100%;
  display: flex;
  &__wrapper {
    width: 100%;
    padding: 13px 20px 35px;
    overflow: hidden;
  }
  &__container {
    height: calc(100% - 80px);
    width: 100%;
    display: flex;
    flex: 1;
    -webkit-box-shadow: 0px 0px 17px -1px rgba(34, 60, 80, 0.21);
    -moz-box-shadow: 0px 0px 17px -1px rgba(34, 60, 80, 0.21);
    box-shadow: 0px 0px 17px -1px rgba(34, 60, 80, 0.21);
  }
  &__content {
    min-height: 100%;
    padding: 13px 20px 35px;
    background-color: #fff;
    flex-grow: 1;
    position: relative;
  }
  @media (max-width: 800px) {
    &__wrapper {
      padding-left: 10px;
      padding-right: 10px;
    }
  }
}
</style>
