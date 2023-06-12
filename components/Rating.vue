<script setup>
const rating = ref([]);
const props = defineProps({
  ratings: {
    type: Number,
    default: 0,
  },
});

onMounted(() => {
  for (let i = 1; i <= 5; i++) {
    const icon =
      i <= props.ratings ? "ic:round-star-rate" : "ic:round-star-border";
    rating.value.push({ icon });
  }
});
</script>
<template>
  <div>
    <span v-for="(rate, index) in rating" :key="index"
      ><Icon :name="rate.icon" class="filled"
    /></span>
  </div>
</template>
