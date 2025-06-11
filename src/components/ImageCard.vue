<template>
  <div class="card" @click="$emit('click')">
    <img :src="src" alt="graffiti tag" class="card-image" />
    <div class="card-date">{{ date }}</div>
  </div>
</template>

<script setup>
defineProps({
  src: String,
  date: String,
})
defineEmits(['click'])
</script>

<style scoped>
.card {
  background-color: #222;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.7);
  height: 240px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: scale(1.03);
}

.card-image {
  width: 100%;
  height: 200px;
  object-fit: contain;
  background-color: #000;
  display: block;
}

.card-date {
  text-align: center;
  padding: 0.5rem;
  color: #aaa;
  font-size: 0.9rem;
  background-color: #1a1a1a;
}
</style>
