<template>
  <div class="todo-list-container">
    <TodoInputComponent @addNewTodo="addtodo" />

    <TodoComponent
      v-for="(todo, index) in todolist"
      :todo="todo.text"
      :status="todo.isCompleted"
      :key="todo"
      @checked="onChecked($event, index)"
    />
  </div>
</template>
<script>
import TodoComponent from "./components/TodoComponent.vue";
import TodoInputComponent from "./components/TodoInputComponent.vue";
export default {
  components: {
    TodoComponent,
    TodoInputComponent,
  },
  data() {
    return {
      todolist: [
        { text: "buy milk", isCompleted: true },
        { text: "go to school", isCompleted: false },
      ],
    };
  },
  methods: {
    addtodo(todoText) {
      this.todolist.push({
        text: todoText,
        isCompleted: false,
      });
    },
    onChecked(isChecked, index) {
      this.todolist[index].isCompleted = isChecked;
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background: linear-gradient(135deg, #f5af19, #f12711);
  width: 100%;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
</style>
<style scoped>
.todo-list-container {
  margin: 10px 20px;
  display: flex;
  flex-direction: column;
  padding: 10px;
  background-color: white;
  border-radius: 5px;
  width: 100%;
}
</style>