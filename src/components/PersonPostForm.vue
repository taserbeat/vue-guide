<script setup lang="ts">
import { ref } from "vue";

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
</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-column">
        <span>name:</span>
        <input class="input" v-model="inputName" />
      </div>

      <div class="input-column">
        <span>age:</span>
        <input class="input" v-model="inputAge" type="number" />
      </div>
    </div>

    <button class="register-button" @click="handleRegister">register</button>
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

input {
  width: 120px;
  margin-bottom: 8px;
}

span {
  font-size: 20px;
  font-weight: bold;
}
</style>
