<template>
  <div>
    <img v-bind:src="require('./picture.jpg')" alt="" />
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
img {
  width: 100px;
  align-items: center;
  border-radius: 10px;
  box-shadow: 0px 0px 18px 8px rgba(214, 64, 126, 0.81);
}
</style>
