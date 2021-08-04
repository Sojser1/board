<template>
  <div class="todolist">
    <v-card-line
      :items="col1"
      title="need to do"
      :color="colors.rowOne"
      @changeList="saveChanges"
      @removeCard="removeCard"
    ></v-card-line>
    <v-card-line
      :items="col2"
      title="in the process"
      :color="colors.rowTwo"
      @changeList="saveChanges"
      @removeCard="removeCard"
    ></v-card-line>
    <v-card-line
      :items="col3"
      title="finished"
      :color="colors.rowThree"
      @changeList="saveChanges"
      @removeCard="removeCard"
    ></v-card-line>
    <v-card-line
      :items="col4"
      title="verified"
      :color="colors.rowFour"
      @changeList="saveChanges"
      @removeCard="removeCard"
    ></v-card-line>
  </div>
</template>

<script>
import vCardLine from './components/v-card-line.vue'
import { colorsOptionst } from './options/color.js'
export default {
  created() {
    this.loadlist()
    this.colors = colorsOptionst()
  },
  components: { vCardLine },
  data() {
    return {
      drag: false,
      list: null,
      colors: null,
    }
  },
  methods: {
    loadlist() {
      const todolist = JSON.parse(localStorage.getItem('todolist'))
      if (todolist) {
        this.list = todolist
      } else {
        this.list = { st: [], nd: [], rd: [], fth: [] }
      }
    },
    saveChanges() {
      const changedList = JSON.stringify(this.list)
      localStorage.setItem('todolist', changedList)
    },
    removeCard(id) {
      for (let col in this.list) {
        this.list[col].forEach((el) => {
          if (el.id === id) {
            const idx = this.list[col].findIndex((card) => {
              return card.id === id
            })
            this.list[col].splice(idx, 1)
          }
        })
      }
    },
  },
  computed: {
    col1() {
      if (this.list) {
        return this.list.st
      }
      return []
    },
    col2() {
      if (this.list) {
        return this.list.nd
      }
      return []
    },
    col3() {
      if (this.list) {
        return this.list.rd
      }
      return []
    },
    col4() {
      if (this.list) {
        return this.list.fth
      }
      return []
    },
  },
}
</script>

<style src="./index.css"></style>
