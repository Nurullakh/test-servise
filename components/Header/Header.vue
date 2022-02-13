<template>
  <header class="header">
    <label class="header__input">
      <input type="text" placeholder="Поиск" />
    </label>
    <div class="header__user">
      <div class="header__avatar-wrapper">
        <img
          class="header__avatar"
          src="~@/assets/img/avatar.png"
          alt="avatar"
        />
      </div>
      <div class="header__user-about">
        <span class="header__name">Nurullakh A.</span>
        <span class="header__status">Администратор</span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: null,
    },
    img: {
      type: String,
      default: null,
    },
  },
}
</script>

<style lang="scss" scoped>
.header {
  margin-bottom: 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  &__input {
    position: relative;
    display: flex;
    align-items: center;
    padding: 0 14px;
    border: 1px solid #e5e5e5;
    background-color: #fff;
    border-radius: 4px;
    overflow: hidden;
    box-sizing: border-box;
    cursor: text;
    flex: 0.8;
    input {
      width: 100%;
      height: 39px;
      border: none;
      padding: 5px 0;
      font-size: 14px;
      line-height: 16px;
      background-color: transparent;
      color: #000;
      outline: none;
      -webkit-appearance: none;
      box-sizing: border-box;
    }
    &:after {
      content: '';
      display: inline-block;
      width: 16px;
      height: 16px;
      margin-left: 4px;
      flex-shrink: 0;
      vertical-align: middle;
      background-repeat: no-repeat;
      background-position: center;
      background-size: contain;
      background-image: url(~@/assets/img/search.svg);
    }
  }
  &__user {
    display: flex;
    align-items: center;
  }
  &__avatar-wrapper {
    margin-right: 3px;
    border-radius: 50%;
    flex-shrink: 0;
    width: 50px;
    height: 50px;
  }
  &__avatar {
    width: 100%;
    height: 100%;
  }
  &__name {
    display: block;
    max-width: 150px;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
    font-size: 18px;
    line-height: 21px;
    font-weight: 500;
  }
  &__status {
    margin-top: 4px;
    display: inline-block;
    font-size: 14px;
    line-height: 17px;
  }
}
</style>
