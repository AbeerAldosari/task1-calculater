<!-- NumberButtonRow.vue -->
<template>
  
    <td @click="onClick" class="btn-number">
      <i :class="`fa-solid fa-${number}`"></i>
    </td>
  </template>
  
  <script>
  export default {
    props: {
      number: {
        type: String,
        required: true,
      },
    },
    methods: {
      onClick() {
        this.$emit('number-clicked', this.number);
      },
    },
  };
  </script>
  <style>
   td {
  cursor: pointer;
  text-align: center;
  font-size: 24px;
  padding: 15px;
  transition: background-color 0.2s ease;
}
td:hover {
  background-color: #f0f0f0;
}
</style>