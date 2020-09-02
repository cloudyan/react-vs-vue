<template>
  <div class="todo-item">
    <p class="todo-item__text">{{item.text}}</p>
    <button class="todo-item__delete" @click="deleteItem(item.id)">-</button>
  </div>
</template>

<script>
export default {
  name: 'ToDoItem',
  props: ['item'],
  setup(props, { emit }) {
    function deleteItem(id) {
      emit('delete', id);
    }
    return {
      deleteItem,
    };
  }
};
</script>

<style lang="less" scoped>
.todo-item {
  display: flex;
  justify-content: center;
  align-items: center;

  &__text {
    width: 90%;
    padding: 12px;
    margin-right: 10px;
    border-radius: 4px;
    border-color: rgba(0, 0, 0, 0.5);
    background: #ffffff;
    box-shadow: 5px 5px 13px #d9d9d9, -5px -5px 13px #ffffff;
    text-align: left;
  }

  &__delete {
    width: 50px;
    height: 50px;
    border-radius: 10px;
    background: linear-gradient(145deg, #e6e6e6, #ffffff);
    box-shadow: 5px 5px 15px #cccccc, -5px -5px 15px #ffffff;
    border-color: transparent;
    color: red;
    font-size: 2rem;
    cursor: pointer;
  }

  &__delete:hover {
    box-shadow: 5px 5px 10px #cccccc, -5px -5px 10px #ffffff;
  }
}
</style>
