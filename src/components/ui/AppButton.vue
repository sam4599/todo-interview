<template>
  <div>
    <button class="button"@click="$emit('click')">СОЗДАТЬ</button>
  </div>
</template>

<script>
export default {
  name: 'AppButton'
}
</script>

<style scoped>
.button {
  padding: 10px 20px;
  background: transparent;
  color: #FFFFFF;
  border-color: #FFFFFF;
}
</style>