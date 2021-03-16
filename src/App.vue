<template>
  <v-app>
    <v-container class="pa-12">
      <div class="mb-4 text-body">
        You have {{ todoList.length }} todo items
      </div>
      <v-row>
        <v-col class="flex-grow-1 mb-7">
          <v-card
            v-for="todo in todoList"
            :key="todo.label"
            elevation="2"
            class="pa-6 mb-4"
          >
            <v-checkbox v-model="todo.checked">
              <template slot="label">
                <div class="pl-4">
                  <div class="text-h6">{{ todo.label }}</div>
                  <div>{{ todo.description }}</div>
                </div>
              </template>
            </v-checkbox>
          </v-card>
        </v-col>
        <v-col class="mb-5">
          <v-card class="add-btn ml-6 pa-6">
            <v-text-field
              v-model="itemLabel"
              label="Item"
              class="margin-right"
            ></v-text-field>
            <v-text-field
              v-model="itemDescription"
              label="Description"
              class="margin-right"
            ></v-text-field>
            <v-btn @click="addItem" block color="primary">
              Add todo
            </v-btn>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
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
        checked: false,
      },
      {
        label: "Todo2",
        description: "todo description",
        checked: false,
      },
    ];

    const itemLabel = ref("");
    const itemDescription = ref("");

    const addItem = () => {
      if (itemLabel.value) {
        todoList.value.push({
          label: itemLabel.value,
          description: itemDescription.value,
          checked: false,
        });
      }
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
