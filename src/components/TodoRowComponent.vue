<template>
  <div class="todo-container">
    <input
      type="checkbox"
      :checked="status"
      name="work status"
      @change="emitCheckedEvent($event)"
    />
    <h4 :class="{ 'line-through': status }">{{ todo }}</h4>
    <Icon icon="ci:more-horizontal" />
  </div>
</template>
<script>
import { Icon } from "@iconify/vue";
export default {
  components: {
    Icon,
  },
  props: {
    todo: String,
    status: {
      type: Boolean,
    },
  },
  methods: {
    emitCheckedEvent() {
      this.$emit("checked");
    },
  },
};
</script>
<style scoped>
.todo-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 10px 20px;
  padding: 10px 0;
}

.todo-container h4 {
  flex: 1;
  margin-left: 10px;
}
.line-through {
  text-decoration: line-through;
}
</style>