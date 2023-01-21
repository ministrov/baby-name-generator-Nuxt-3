<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p @click="removeName">x</p>
  </div>
</template>

<script setup lang="ts">

interface NameProps {
  name: string
  index: number
}

const props = defineProps<NameProps>();

const emit = defineEmits(["remove"]);

const removeName = () => {
  emit("remove", props.index)
}
</script>

<style scoped>
.card {
  position: relative;
  width: 28%;
  margin-right: 0.4rem;
  margin-bottom: 1rem;
  padding: 0.1rem;
  color: white;
  background-color: rgb(27, 60, 138);
  border-radius: 1rem;
}

.card p {
  position: absolute;
  top: -17%;
  left: 91.5%;
  color: rgba(255, 255, 255, 0.178);
  cursor: pointer;
}
</style>