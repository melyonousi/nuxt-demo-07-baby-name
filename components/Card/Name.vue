<template>
  <div class="card">
    <h4 v-text="name" />
    <p v-text="'X'" @click="removeName()"></p>
  </div>
</template>

<script setup lang="ts">
interface NameProps {
  name: string;
  index: number;
}
const props = defineProps<NameProps>();
const emit = defineEmits(["remove"]);

const removeName = () => {
  emit("remove", props.index);
};
</script>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 30%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  position: relative;
  margin: auto;
}

.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  cursor: pointer;
  color: rgb(255, 255, 255, 0.178);
}
</style>
