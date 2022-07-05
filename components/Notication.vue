<template>
  <div class="bg-red-500 text-white w-3/4 h-3/4">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: 'Notification',
  props: ['message'],
};
</script>
