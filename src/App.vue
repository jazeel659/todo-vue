<template>
  <div class="todo-list-container">
    <TodoInputComponent @addNewTodo="addtodo" />
    <section class="filter-bar">
      <ul>
        <li
          v-for="filter in filterModes"
          :key="filter"
          :class="{ active: selectedFilter == filter }"
          @click="chooseFilter(filter)"
        >
          {{ filter }}
        </li>
      </ul>
      <button @click="clearAll">Clear All</button>
    </section>
    <p class="no-data-message" v-if="actualTodo.length == 0">
      {{ noDataInfoMessage }}
    </p>
    <TodoRowComponent
      v-for="todo in actualTodo"
      :todo="todo.text"
      :status="todo.isCompleted"
      :key="todo"
      @checked="onChecked(todo.id)"
    />
  </div>
</template>
<script>
import TodoRowComponent from "./components/TodoRowComponent.vue";
import TodoInputComponent from "./components/TodoInputComponent.vue";
import { v4 as uuidv4 } from "uuid";
export default {
  components: {
    TodoRowComponent,
    TodoInputComponent,
  },
  data() {
    return {
      todolist: [],
      filterModes: ["All", "Pending", "Completed"],
      selectedFilter: "All",
      myName: "jaseel",
    };
  },
  computed: {
    getPendingTodos() {
      return this.todolist.filter((todo) => {
        return todo.isCompleted == false;
      });
    },

    getCompletedTodos() {
      return this.todolist.filter((todo) => {
        return todo.isCompleted == true;
      });
    },
    modifiedName() {
      return "my name is" + this.myName;
    },
    actualTodo() {
      if (this.selectedFilter == "All") {
        return this.todolist;
      } else if (this.selectedFilter == "Pending") {
        return this.getPendingTodos;
      } else if (this.selectedFilter == "Completed") {
        return this.getCompletedTodos;
      }
    },
    noDataInfoMessage() {
      if (this.selectedFilter == "All") {
        return "You dont have any task😎";
      } else if (this.selectedFilter == "Pending") {
        return "You dont have any pending task🎉";
      } else if (this.selectedFilter == "Completed") {
        return "You dont have any completed task😒";
      }
    },
  },
  methods: {
    addtodo(todoText) {
      this.todolist.unshift({
        text: todoText,
        isCompleted: false,
        id: uuidv4(),
      });
    },
    onChecked(id) {
      let index = this.todolist.findIndex((todo) => todo.id == id);
      this.todolist[index].isCompleted = !this.todolist[index].isCompleted;
    },
    chooseFilter(filter) {
      this.selectedFilter = filter;
    },
    clearAll() {
      this.todolist = [];
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
  font-family: sans-serif;
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

  background-color: white;
  border-radius: 5px;
  width: 100%;
}
.todo-list-container .filter-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  font-size: 20px;
  border-bottom: 1px solid #4444;
}

.todo-list-container .filter-bar ul {
  list-style: none;
  display: flex;
  justify-content: space-between;
  flex: 1;
  margin-right: 100px;
  color: #444;
  font-weight: 300;
}
.todo-list-container .filter-bar ul li.active {
  color: #f12711;
}
.todo-list-container .filter-bar ul li:hover {
  cursor: pointer;
}
.todo-list-container .filter-bar button {
  background: linear-gradient(135deg, #f5af19, #f12711);
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
  padding: 10px;
}
@media (max-width: 480px) {
  .todo-list-container .filter-bar ul {
    margin-right: 10px;
  }
}

.todo-list-container .no-data-message {
  padding: 18px 15px;
  font-size: 20px;
}
</style>