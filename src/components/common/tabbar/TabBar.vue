<template>
  <div id="tab_bar">
    <slot></slot>
  </div>
</template>

<script>
    export default {
        name: "TabBar"
    }
</script>

<style scoped>


  #tab_bar{
    display: flex;
    position: fixed;
    left: 0px;
    right: 0px;
    bottom: 0px;
    height: 49px;
    background-color: #f6f6f6;

    box-shadow: 0px -2px 1px rgba(100,100,100,0.1);
  }



</style>
