<template>
  <header class="header">
    <div class="global-container container">
      <p>TO<span>DO</span>S</p>
      <create-modal @send-todo="sendData"/>
    </div>
  </header>
</template>

<script>
import CreateModal from "@/components/CreateModal.vue";

export default {
  name: 'TheHeader',
  components: {
    CreateModal
  },
  methods: {
    sendData(data) {
      this.$emit('add-todo', data)
    }
  }
}
</script>

<style scoped>
.header {
  background: #000000FF;
}
.container {
  display: flex;
  justify-content: space-between;
  padding: 12px 0;
  align-items: center;
}
.global-container p {
  color: #FFFFFF;
  font-size: 18px;
}
p span {
  color: #FC5151;
}
</style>