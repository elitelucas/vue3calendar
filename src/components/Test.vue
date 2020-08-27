<template>
  <div>
    <h1>{{msg}}</h1>
    <h3>{{title}}</h3>
    <p>Capacity: {{ capacity }}</p>
    <button @click="increaseCapacity()">Increase Capacity</button>
  </div>
</template>

<script>
import { ref } from "vue"; // <-- Use this line if you're in a Vue 3 app

export default {
  props: {
    msg: String,
  },
  setup() {
    const capacity = ref(3);
    const title = ref("Test");

    function increaseCapacity() {
      capacity.value++;
    }
    return { title, capacity, increaseCapacity };
  },
};
</script>