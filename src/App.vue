<template>
  <div class="todo-list-container">
    <div class="todo-input">
      <Icon class="compose" icon="fluent:compose-16-filled" />
      <input type="text" placeholder="add new task" @keyup.enter="addtodo" />
    </div>
    <todocomponent
      v-for="todo in todolist"
      :todo="todo.todo"
      :status="todo.isCompleted"
      :key="todo"
      @checked="onChecked"
    />
  </div>
</template>
<script>
import todocomponent from "./components/todocomponent.vue";
import { Icon } from "@iconify/vue";

export default {
  components: {
    todocomponent,
    Icon,
  },
  data() {
    return {
      todolist: [
        { todo: "buy milk", isCompleted: true },
        { todo: "go to school", isCompleted: false },
      ],
    };
  },
  methods: {
    addtodo($event) {
      if ($event.srcElement.value != "") {
        this.todolist.push({
          todo: $event.srcElement.value,
          isCompleted: false,
        });
        $event.srcElement.value = "";
      }
    },
    onChecked($event) {
      console.log($event);
      const index = this.todolist.findIndex(
        (todoElement) => todoElement.todo == $event.todoText
      );
      this.todolist[index].isCompleted = $event.checked;
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

.todo-input {
  display: flex;
  align-items: center;
  border: 1px solid #666a;
  padding: 10px;
  border-radius: 5px;
}

.todo-input input {
  height: 40px;
  flex: 1;
  border: none;
  outline: none;
  margin-left: 20px;
  font-size: 18px;
}

.todo-input .compose {
  font-size: 20px;
  color: #666a;
}

.todo-input:focus-within {
  border: 2px solid red;
}
</style>