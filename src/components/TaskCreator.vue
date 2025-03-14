<template>
  <div class="task-creator" v-if="!isBusy">
    <button class="task-creator__plus-button" @click="addItemToTaskList">
      <div class="task-creator__circle">
        <PlusIcon class="task-creator__plus-icon" />
      </div>
    </button>
    <input
      type="text"
      class="task-creator__input"
      placeholder="Create a new todo..."
      v-model="text"
    />
  </div>
  <div v-else class="busy">
    <BusyIcon class="busy-icon" />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

import PlusIcon from "../assets/PlusIcon.vue";
import BusyIcon from "../assets/BusyIcon.vue";

import { TaskContent } from "../types/type";
import { useTodoStore } from "../store/todoStore";

const todoStore = useTodoStore();

const text = ref("");

const isBusy = computed(() => todoStore.isLoading);

async function addItemToTaskList() {
  try {
    if (text.value !== "") {
      const newTask: TaskContent = {
        content: text.value,
        state: "active",
      };

      const data = await todoStore.addTask(newTask);
      if (data) {
        text.value = "";
      }
    }
  } catch (err) {}
}
</script>

<style lang="scss">
.task-creator {
  background-color: var(--very-dark-desaturated-blue);
  padding: 8px 20px;

  color: white;
  display: flex;
  gap: 14px;
  align-items: center;
  box-shadow: rgba(0, 0, 0, 0.07) 0px 1px 2px, rgba(0, 0, 0, 0.07) 0px 2px 4px,
    rgba(0, 0, 0, 0.07) 0px 4px 8px, rgba(0, 0, 0, 0.07) 0px 8px 16px,
    rgba(0, 0, 0, 0.07) 0px 16px 32px, rgba(0, 0, 0, 0.07) 0px 32px 64px;

  &__input {
    background-color: transparent;
    border: none;
    color: var(--light-grayish-blue-dark-mode);
    font-weight: 400;
    font-size: 18px;
    width: 100%;
    font-family: "Josefin Sans", sans-serif;
    margin: 1em;
    margin-left: 8px;

    &::placeholder {
      color: var(--dark-grayish-blue-dark-mode);
    }

    &:focus {
      outline: none;
    }
  }
}

.task-creator__plus-button {
  background: none;
  border: none;
  cursor: pointer;
  border-radius: 50%;
  padding: 1px;
  background-color: var(--very-dark-grayish-blue-dark-mode);
  display: flex;
  align-items: center;
  justify-content: center;

  .task-creator__plus-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    fill: var(--light-grayish-blue-dark-mode);
  }

  &:hover {
    background-image: linear-gradient(
      150deg,
      hsl(192, 100%, 67%),
      hsl(280, 87%, 65%)
    );
    .task-creator__plus-icon {
      fill: white;
    }
  }
}

.task-creator__circle {
  border-radius: 50%;
  padding: 6px 7px;
  background-color: var(--very-dark-desaturated-blue);
}

.busy {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--very-dark-desaturated-blue);
  padding: 29px 0px;
  box-shadow: rgba(0, 0, 0, 0.07) 0px 1px 2px, rgba(0, 0, 0, 0.07) 0px 2px 4px,
    rgba(0, 0, 0, 0.07) 0px 4px 8px, rgba(0, 0, 0, 0.07) 0px 8px 16px,
    rgba(0, 0, 0, 0.07) 0px 16px 32px, rgba(0, 0, 0, 0.07) 0px 32px 64px;
}
</style>
