<template>
  <div class="create-survey">
    <button class="button create-survey__add" @click.stop="add">
      Добавить условие
    </button>
    <ValidationObserver v-slot="{ handleSubmit }">
      <form
        class="create-survey__form"
        @submit.prevent="handleSubmit(() => submit(surveyList))"
      >
        <div class="create-survey__content">
          <transition-group name="fade">
            <div
              v-for="(survey, index) in surveyList"
              :key="survey.id"
              :class="[
                'create-survey__item',
                { [`create-survey__item_${survey.type}`]: survey.type },
              ]"
            >
              <div class="create-survey__item-row create-survey__item-row_top">
                <div
                  class="create-survey__item-col create-survey__item-col_left"
                >
                  <h4 class="create-survey__item-title">
                    Условие {{ index + 1 }}
                  </h4>
                </div>
                <div class="create-survey__item-col">
                  <ValidationProvider v-slot="{ errors }" rules="required">
                    <select
                      v-model="survey.type"
                      :class="['create-survey__select', { error: errors[0] }]"
                    >
                      <option :value="null">Выберите условие</option>
                      <option
                        v-for="option in list"
                        :key="option.type"
                        :value="option.type"
                      >
                        {{ option.text }}
                      </option>
                    </select>
                  </ValidationProvider>
                </div>
              </div>
              <div v-if="survey.type === 'age'" class="create-survey__item-row">
                <div
                  class="create-survey__item-col create-survey__item-col_left"
                >
                  Диапозон 1
                </div>
                <div class="create-survey__item-col">
                  от
                  <ValidationProvider v-slot="{ errors }" rules="required">
                    <label
                      :class="['create-survey__input', { error: errors[0] }]"
                    >
                      <input v-model="survey.data.from" type="number" />
                    </label>
                  </ValidationProvider>
                  до
                  <ValidationProvider v-slot="{ errors }" rules="required">
                    <label
                      :class="['create-survey__input', { error: errors[0] }]"
                    >
                      <input v-model="survey.data.to" type="number" />
                    </label>
                  </ValidationProvider>
                </div>
              </div>
              <div
                v-else-if="survey.type === 'type'"
                class="create-survey__item-row"
              >
                <div
                  class="create-survey__item-col create-survey__item-col_left"
                >
                  Тип 1
                </div>
                <div class="create-survey__item-col">
                  <ValidationProvider v-slot="{ errors }" rules="required">
                    <select
                      v-model="survey.data.type"
                      :class="['create-survey__select', { error: errors[0] }]"
                    >
                      <option
                        v-for="option in [
                          { type: 'gold', text: 'Gold', selected: true },
                          { type: 'black', text: 'Black' },
                        ]"
                        :key="option.type"
                        :value="option.type"
                        :selected="{ selected: option.selected }"
                      >
                        {{ option.text }}
                      </option>
                    </select>
                  </ValidationProvider>
                </div>
              </div>
              <div
                v-else-if="survey.type === 'status'"
                class="create-survey__item-row"
              >
                <div
                  class="create-survey__item-col create-survey__item-col_left"
                >
                  Статус 1
                </div>
                <div class="create-survey__item-col">
                  <ValidationProvider v-slot="{ errors }" rules="required">
                    <select
                      v-model="survey.data.status"
                      :class="['create-survey__select', { error: errors[0] }]"
                    >
                      <option
                        v-for="option in [
                          { type: 'active', text: 'Активна' },
                          { type: 'close', text: 'Закрыта' },
                        ]"
                        :key="option.type"
                        :value="option.type"
                      >
                        {{ option.text }}
                      </option>
                    </select>
                  </ValidationProvider>
                </div>
              </div>
              <div
                class="create-survey__item-row create-survey__item-row_bottom"
              >
                <div
                  class="create-survey__item-col create-survey__item-col_left"
                ></div>
                <div class="create-survey__item-col">
                  <button
                    class="button button_red"
                    type="button"
                    @click.stop="remove(survey.id)"
                  >
                    Удалить
                  </button>
                </div>
              </div>
            </div>
          </transition-group>
        </div>
        <button
          v-if="surveyList.length"
          class="button create-survey__btn-create"
        >
          Создать
        </button>
      </form>
    </ValidationObserver>
    <div v-if="submited" class="create-survey__success">Опрос создан</div>
  </div>
</template>

<script>
import { ValidationProvider, ValidationObserver } from 'vee-validate'

export default {
  components: {
    ValidationProvider,
    ValidationObserver,
  },
  props: {
    /**
     * Состояние успешной отправки
     */
    success: {
      type: Boolean,
    },
  },
  data() {
    return {
      list: [
        { text: 'Возвраст', type: 'age' },
        { text: 'Тип карты', type: 'type' },
        { text: 'Статус карты', type: 'status' },
      ],
      surveyList: [],
      resetWatcher: null,
      submited: false,
    }
  },
  watch: {
    success(val) {
      if (val) {
        this.surveyList = []
        this.submited = true
        this.resetWatcher = this.$watch(
          'surveyList',
          function () {
            this.submited = false
            this.resetWatcher()
          },
          {
            deep: true,
          }
        )
      }
    },
  },
  methods: {
    submit(data) {
      const totalData = {}
      data.forEach((el, index) => {
        totalData[`survey${index + 1}`] = el.data
      })
      this.$emit('submit', totalData)
    },
    add() {
      const survey = {
        id: +String(Math.random()).slice(2),
        type: null,
        data: {},
      }
      this.surveyList.push(survey)
    },
    remove(id) {
      const index = this.surveyList.findIndex((survey) => survey.id === id)
      this.$delete(this.surveyList, index)
    },
  },
}
</script>

<style lang="scss" scoped>
.create-survey {
  &__add {
    width: 100%;
    margin-bottom: 40px;
  }
  &__item {
    padding: 10px 20px 40px;
    background-color: #ebebeb;
    &_age {
      background-color: rgb(255 241 173 / 97%);
      .create-survey__item-title {
        color: rgb(255 181 0 / 97%);
      }
    }
    &_type {
      background-color: rgb(235 219 246 / 97%);
      .create-survey__item-title {
        color: rgb(208 139 255 / 97%);
      }
    }
    &_status {
      background-color: rgb(223 255 237 / 97%);
      .create-survey__item-title {
        color: rgba(77, 235, 148, 0.966);
      }
    }
  }
  &__item-row {
    display: flex;
    align-items: center;
    &_top {
      margin-bottom: 30px;
    }
    &_bottom {
      margin-top: 30px;
    }
  }
  &__item-col {
    flex-grow: 1;
    &_left {
      flex-grow: 0;
      width: 30%;
    }
  }
  &__select {
    width: 100%;
    height: 40px;
  }

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
  }
  &__btn-create {
    margin-top: 20px;
  }
  &__success {
    font-size: 27px;
    font-weight: 500;
    color: #11c86f;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>
