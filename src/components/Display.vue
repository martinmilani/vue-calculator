<template>
  <div class="bg-gradient-to-r from-pink-500 via-red-500 to-yellow-400 h-40">
    <h1 class="text-5xl font-medium text-white text-right pt-8 pb-6 pr-4">
      {{ display }}
    </h1>
    <h3 class="text-2xl font-normal text-white text-right pr-5 opacity-75">
      {{ equation }}
    </h3>
  </div>
</template>

<script>
export default {
  props: ["display", "equation"],
};
</script>

<style></style>
