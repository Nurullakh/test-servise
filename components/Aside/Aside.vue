<template>
  <aside class="aside">
    <nuxt-link to="/">
      <div class="aside__logo"></div>
    </nuxt-link>
    <nav class="aside__nav">
      <nuxt-link
        v-for="el in navList"
        :key="el.name"
        :to="el.url"
        class="aside__nav-el"
        exact-active-class="aside__nav-el_active"
      >
        <img :src="el.src" alt="" class="aside__nav-el-img" />
        <span class="aside__nav-el-text">
          {{ el.name }}
        </span>
      </nuxt-link>
    </nav>
  </aside>
</template>

<script>
export default {
  data() {
    return {
      navList: [
        { name: 'Опросы', url: '/', src: require('~/assets/img/survey.png') },
        {
          name: 'Полльзователи',
          url: '/users/',
          src: require('~/assets/img/users.png'),
        },
        {
          name: 'Черные списки',
          url: '/blacklists/',
          src: require('~/assets/img/blacklist.png'),
        },
        {
          name: 'Колл-центр',
          url: '/call/',
          src: require('~/assets/img/call.png'),
        },
      ],
    }
  },
}
</script>

<style lang="scss" scoped>
.aside {
  width: 140px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-right: 1px solid #ccffcc;
  padding: 15px 10px;
  &__logo-wrapper {
    margin-bottom: 40px;
  }
  &__logo {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: #ccffcc;
    margin-bottom: 20px;
  }
  &__nav {
    position: sticky;
    top: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  &__nav-el {
    margin-bottom: 10px;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 5px;
    padding: 10px;
    &_active {
      background: #ccffcc;
    }
  }
  &__nav-el-img {
    margin-bottom: 5px;
    width: 40px;
  }
  &__nav-el-text {
    font-size: 13px;
  }
}
</style>
