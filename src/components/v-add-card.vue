<template>
  <div class="todolist-item-body-post">
    <textarea
      v-model="cardValue"
      type="text"
      placeholder="Введите задачу"
      @keydown.enter="saveNewCard"
    ></textarea>
  </div>
  <div class="todolist__card-footer">
    <div class="todolist__card-footer-button btn" @click="saveNewCard">
      <span class="close"><b>+</b></span>
      Добавить карточку
    </div>
  </div>
</template>

<script>
export default {
  emits: ['addNewCard'],
  data() {
    return {
      cardValue: '',
    }
  },
  methods: {
    saveNewCard() {
      this.$emit('addNewCard', this.cardValue)
    },
  },
}
</script>

<style scoped>
.todolist-item-body-post {
  margin-top: 5px;
  background-color: #505050;
}

.todolist-item-body-post textarea {
  padding: 10px;
  color: white;
  width: 90%;
  height: 90px;
  background-color: #505050;
  overflow: hidden;
  outline: none;
  resize: none;
  border: none;
}

.todolist-item-button {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
  height: 30px;
  cursor: pointer;
  transition: 0.2s;
  color: #606266;
  position: relative;
}

.todolist-item-button:hover {
  background-color: #26282c;
  transition: 0.3s;
}

.todolist-item-button {
  font-size: 12px;
  display: flex;
}
</style>
