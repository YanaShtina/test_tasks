<template>
  <button 
      class="btn"
      >
      <slot></slot>
    </button>
</template>

<script>
export default {
  name: 'app-btn'
}
</script>

<style lang="scss">
.btn {
  font-size: 14px;
  color: #fff;
  background-color: $a-blue;
  outline: none;
  border: transparent;
  border-radius: 4px;
  padding: 10px;
  align-self: flex-end;

  &:hover {
    cursor: pointer;
    background-color: #0b5ed7;
  }
}

</style>