<script setup lang="ts">
import { computed, ref } from "vue";

const inputName = ref<string>("");
const inputAge = ref<number>(0);

const emit = defineEmits(["register"]);

const handleRegister = () => {
  const person = {
    id: Math.random(),
    name: inputName.value,
    age: inputAge.value,
  };

  emit("register", person);

  inputName.value = "";
  inputAge.value = 0;
};

const maxNameLength = 14;

const isValidName = computed(() => inputName.value.length <= maxNameLength);

const color = computed(() =>
  isValidName.value ? "white" : "rgb(244,194,190)"
);
</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-column">
        <span>name:</span>
        <input class="input-name" v-model="inputName" />
      </div>
      <span class="error-message" v-if="!isValidName"
        >name length must be {{ maxNameLength }} or less</span
      >

      <div class="input-column">
        <span>age:</span>
        <input class="input" v-model="inputAge" type="number" />
      </div>
    </div>

    <button
      class="register-button"
      @click="handleRegister"
      :disabled="!isValidName"
    >
      register
    </button>
  </div>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(255, 241, 226);
  padding: 24px 0;
  width: 50%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.input-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 50px;
  margin-bottom: 20px;
}

.input-column {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

.input-name {
  background-color: v-bind(color);
}

.error-message {
  font-size: 12px;
  color: rgb(244, 194, 190);
}

input {
  width: 120px;
  margin-bottom: 8px;
}

span {
  font-size: 20px;
  font-weight: bold;
}
</style>
