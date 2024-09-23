<template>
  <span>({{ formattedDate }})</span>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'CurrentDate',
  setup() {
    const formattedDate = ref('');

    const updateDate = () => {
      const now = new Date();
      formattedDate.value = now.toLocaleDateString(undefined, {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      });
    };

    onMounted(() => {
      updateDate();
      // If you need the date to refresh daily, set an interval
      // setInterval(updateDate, 86400000); // updates every 24 hours
    });

    return {
      formattedDate
    };
  }
};
</script>

<style scoped>
/* Optional styling */
</style>
