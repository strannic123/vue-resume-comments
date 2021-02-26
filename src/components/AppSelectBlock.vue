<template>
  <form class="card card-w30" @submit.prevent="submitHandler">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea
          id="value"
          rows="3"
          v-model.trim="value"

      ></textarea>
    </div>

    <button class="btn primary" :disabled="!isValid" >Добавить</button>
  </form>
</template>

<script>
export default {
  name: "AppSelectBlock",
  emits: ['block-added'],
  data() {
    return {
      type: 'title',
      value: ''
    }

  },
  computed: {
    isValid() {
      return this.value.length > 3
    }
  },
  methods: {
    submitHandler() {
      this.$emit('block-added', {
        type: this.type,
        value: this.value,
        id: Math.random()
      })
      this.type = 'title'
      this.value = ''
      },

    },

}
</script>

<style scoped>

</style>
