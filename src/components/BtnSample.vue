<template>
  <button>{{ btnname }}</button>
</template>




<script>
  export default {
    name: 'BtnSample',
    props: {
      btnname: String,
      }
    }
</script>




<style scoped>
  button {
    background-color: #00c;
    color: #fff;
    width: 200px;
    border-radius: 5px;
    line-height: 1.8rem;
    text-align: center;
    display: inline-block;
    }
</style>
