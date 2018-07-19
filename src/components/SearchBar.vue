<template>
  <div>
    <input @input="onInput"/>
    <!-- <br><br> -->
    <!-- {{$data}} -->
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data: function () {
    return {
      text: ''
    }
  },
  methods: {
    onInput: function (event) {
      this.$emit('termChange', event.target.value)
    }
  }
}
</script>

<style scoped>
input {
  width: 75%;
}
div {
  text-align: center;
  margin: 20px;
}
</style>
