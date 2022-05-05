<template>
  <div class="inline-flex rounded-md shadow" >
    <a href="#"
      class="inline-flex items-center justify-center px-5 py-1 border border-transparent text-base font-medium rounded-md text-white"
    >
      <slot></slot>
    </a>
  </div>
</template>
<script>
export default {
  name: "MyButton",
};
</script>
<style scoped></style>
