<template>
  
  <div id="header" :style="{backgroundColor: dynamicColors.headerColor}">
    <h1>
        The Great
        <br>
        <span id="colorDisplay">{{dynamicColors.pickedColor}}</span>
        <br> 
        Guessing Game
    </h1>
  </div>

</template>

<script>

  export default  {
    name: 'src-components-header-colores',
    props: ['dynamicColors']
  }

</script>

<style scoped lang="css">  
</style>
