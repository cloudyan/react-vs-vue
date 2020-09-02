<template>
  <div class="todo">
    <img class="logo" :src="logo" alt="Vue logo" />
    <h1 class="todo__header">Vue To Do</h1>
    <div class="todo__container">
      <div class="todo__content">
        <ToDoItem
          v-for="item in list"
          :key="item.id"
          :item="item"
          @delete="onDeleteItem"
        />
      </div>
      <div class="todo__input">
        <input
          type="text"
          placeholder="I need to..."
          v-model="todo"
          v-on:keyup.enter="createNewToDoItem"
        />
        <button class="todo__add" @click="createNewToDoItem">+</button>
      </div>
      <div class="todo__error-container">
        <p v-if="showError">Please enter a todo!</p>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './ToDoItem.vue';
import Logo from '../assets/logo.png';

export default {
  name: 'ToDo',
  components: {
    ToDoItem
  },
  data() {
    return {
      list: [
        { id: 1, text: "clean the house" },
        { id: 2, text: "buy milk" },
      ],
      todo: "",
      logo: Logo
    };
  },

  methods: {
    createNewToDoItem() {
      //validate todo
      if (!this.todo) {
        alert("Please enter a todo!");
        return;
      }

      const newId = this.list.length
        ? Math.max.apply(null, this.list.map(t => t.id)) + 1
        : 1;
      this.list.push({ id: newId, text: this.todo });
      this.todo = "";
    },
    onDeleteItem(id) {
      this.list = this.list.filter(item => item.id !== id);
    }
  }
};
</script>

<style lang="less" scoped>
.logo {
  width: 50px;
  position: relative;
  top: 50px;
}

.todo {
  text-align: center;
  width: 80vw;
  max-width: 768px;
  height: auto;
  margin: 40px auto;
  border-radius: 10px;
  background: #ffffff;

  .todo__input {
    margin-top: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__header {
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
      Arial, sans-serif;
    font-weight: 400;
    text-transform: uppercase;
    margin: 70px auto 30px;
  }

  &__subheader {
    font-size: 1em;
    color: black;
    font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
      Arial, sans-serif;
    font-weight: 400;
    margin: 4px auto 20px;
  }

  &__add {
    cursor: pointer;
    width: 50px;
    height: 50px;
    border-color: transparent;
    color: #73ff73;
    font-size: 2rem;
    border-radius: 10px;
    background: linear-gradient(145deg, #e6e6e6, #ffffff);
    box-shadow: 5px 5px 15px #cccccc, -5px -5px 15px #ffffff;
  }

  &__add:hover {
    box-shadow: 5px 5px 10px #cccccc, -5px -5px 10px #ffffff;
  }

  &__container {
    width: 80%;
    margin: 0 auto;
  }

  &__error-container {
    height: 100px;
    width: 90%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: red;
    font-size: 1rem;
  }
}


</style>
