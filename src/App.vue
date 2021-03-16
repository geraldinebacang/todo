<template>
  <v-app class="padding">
    <v-card
      v-for="todo in todoList"
      :key="todo.label"
      elevation="2"
      class="margin-bottom padding"
    >
      <div>{{ todo.label }}</div>
      <div>{{ todo.description }}</div>
    </v-card>
    <div class="add-btn">
      <v-text-field
        v-model="itemLabel"
        label="Todo Item"
        class="margin-right"
      ></v-text-field>
      <v-btn @click="addItem">
        Add
      </v-btn>
    </div>
  </v-app>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/composition-api";
import TodoItem from "./interface";
export default defineComponent({
  name: "App",
  setup() {
    const todoList = ref<TodoItem[]>([]);
    todoList.value = [
      {
        label: "Todo1",
        description: "todo description",
      },
      {
        label: "Todo2",
        description: "todo description",
      },
    ];

    const itemLabel = ref("");

    const addItem = () => {
      todoList.value.push({
        label: itemLabel.value,
        description: "",
      });
    };

    return {
      todoList,
      itemLabel,
      addItem,
    };
  },
});
</script>
<style lang="css">
.padding {
  padding: 1rem;
}

.margin-bottom {
  margin-bottom: 1rem;
}

.margin-right {
  margin-right: 1rem;
}

.add-btn {
  display: flex;
  align-items: center;
}
</style>
