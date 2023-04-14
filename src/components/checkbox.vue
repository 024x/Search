<template>
  <div class="checkbox-wrapper-33">
    <label class="checkbox">
      <input v-model="updateMessage" type="checkbox" class="checkbox__trigger visuallyhidden">
      <span class="checkbox__symbol">
        <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
          class="icon-checkbox" aria-hidden="true">
          <path d="M4 14l8 7L24 7"></path>
        </svg>
      </span>
      <p class="checkbox__textwrapper">{{ label }}</p>
    </label>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  
  methods: {
    updateMessage() {
      this.$emit('update-message', 'Hello');
    }
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
