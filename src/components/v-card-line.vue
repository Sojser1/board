<template>
  <div class="todolist__card">
    <div class="todolist__card-header">
      <h2 :style="{ 'background-color': color }">
        {{ title }} ({{ itemsLength }})
      </h2>
      <draggable
        :list="todoList"
        class="list-group"
        group="spacedName"
        @change="this.$emit('changeList')"
        @start="drag = true"
        @end="drag = false"
        itemKey="value"
      >
        <template #item="{ element }">
          <div class="todolist__card-item">
            <p><b>id</b> {{ element.id }}</p>
            <p>
              {{ element.value }}
            </p>
            <span class="close" @click="removeCard($event, element.id)"
              ><b>+</b></span
            >
          </div>
        </template>
      </draggable>
      <v-add-card v-if="newCard" @addNewCard="saveNewCard"></v-add-card>
      <div class="todolist__card-footer" @click="addNewCard" v-if="!newCard">
        <div class="todolist__card-footer-button btn">
          <span class="close"><b>+</b></span>
          Добавить карточку
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import draggable from 'vuedraggable'
import VAddCard from './v-add-card.vue'
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    title: {
      type: String,
      required: false,
    },
    color: {
      type: String,
      required: false,
    },
  },
  emits: ['changeList', 'removeCard'],
  data() {
    return {
      drag: false,
      newCard: false,
    }
  },
  components: { draggable, VAddCard },
  methods: {
    addNewCard() {
      this.newCard = true
    },
    saveNewCard(val) {
      this.newCard = false
      if (val.length === 0) {
        return
      }
      const newCard = {
        id: Date.now(),
        value: val,
      }
      this.items.push(newCard)
      this.$emit('changeList')
    },
    removeCard(event, id) {
      this.$emit('removeCard', id)
      this.$emit('changeList')
    },
  },
  computed: {
    todoList() {
      return this.items
    },
    itemsLength() {
      if (this.items) {
        return this.items.length
      }
      return 0
    },
  },
}
</script>

<style></style>
