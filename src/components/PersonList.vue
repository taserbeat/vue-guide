<script setup lang="ts">
import { Person } from "./Persons.vue";

type Props = {
  persons: Person[];
};

defineProps<Props>();

const emit = defineEmits(["delete"]);

const handleDelete = (id: number, name: string) => {
  if (confirm(`Delete ${name}?`)) {
    emit("delete", id);
  }
};
</script>

<template>
  <li class="person-list" v-for="person in persons" :key="person.id">
    <span>{{ person.name }}</span>

    <span>age: {{ person.age }}</span>

    <button class="delete-button" @click="handleDelete(person.id, person.name)">
      delete
    </button>
  </li>
</template>

<style scoped>
.person-list {
  list-style: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 20px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  background-color: rgb(228, 201, 133);
  padding: 8px 20px;
  width: 300px;
}
</style>
