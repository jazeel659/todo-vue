<template>
  <div class="todo-input">
    <Icon class="compose" icon="fluent:compose-16-filled" />
    <input
      type="text"
      placeholder="add new task"
      @keyup.enter="emitInputEvent"
    />
    <button @click="buttonHandler">add</button>
  </div>
</template>

<script>
import { Icon } from "@iconify/vue";

export default {
  components: {
    Icon,
  },
  methods: {
    emitInputEvent($event) {
      if ($event.srcElement.value != "") {
        this.$emit("addNewTodo", $event.srcElement.value);
        $event.srcElement.value = "";
      }
    },
    buttonHandler() {
      this.$emit("addNewTodo", "hi");
    },
  },
};
</script>

<style scoped>
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