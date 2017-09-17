<template>
  <div id="app">
    <h1 style="position: absolute;top: 100px;font-size: 30px;left: 50%;transform: translateX(-50%);">TO DO LIST</h1>
    <input type="text" class="input" v-model="input" @keyup.enter='addEvent'>
    <transition-group name="list" tag="div"> 
      <doing :doing='todolist' v-show="istodo" :dolength='dolength' class="do-group" :key="a"></doing>
      <done class="done-group" :key="b"></done>
    </transition-group>
  </div>
</template>

<script>
import doing from './components/do.vue'
import done from './components/done.vue'

export default {
  name: 'app',
  components: {
    doing,
    done
  },
  data() {
    return {
      input: '',
      todolist: [],
      dolength: '',
      a: 'a',
      b: 'b'
    }
  },
  methods: {
    addEvent: function(e) {
      let todo = this.input.trim()
      this.todolist.push(todo)
      this.input = ''
    }
  },
  computed: {
    istodo: function() {
      if (this.todolist.length !== 0) {
        this.dolength = this.todolist.length
        return true
      } else {
        return false
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  width: 80%;
  display: block;
  margin: 0 auto;
  text-align: center;
  .input {
    display: block;
    width: 80%;
    margin: 0 auto;
    height: 40px;
    line-height: 40px;
    margin-top: 200px;
    border: 1px solid #DCDCDC;
    border-radius: 11px;
    text-align: center;
    font-size: 20px;
  }
  .do-group {

    transition: all 1s;
    display: inline-block;
    text-align: left;
    &.list-enter-active,
    &.list-leave-active {
      transition: all 1s;
      position: absolute;
    }
    &.list-enter,
    &.list-leave-to {
      opacity: 0;
      transform: translateY(30px);
      height: 0;
    }
  }
  .done-group {
    text-align: left;
    transition: all 1s;
    display: inline-block;
    &.list-enter-active,
    &.list-leave-active {
      transition: all 1s;
      position: absolute;
    }
    &.list-enter,
    &.list-leave-to {
      opacity: 0;
      transform: translateY(30px);
      height: 0;
    }
  }
}
</style>
