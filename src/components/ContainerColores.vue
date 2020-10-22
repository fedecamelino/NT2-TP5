<template> 

  <div id="container">
    <SquareColores 
      class="square"
      :index="index"
      :fmensajes="fmensajes" 
      :mensajes="mensajes"
      :fsquare="fsquare"
      :square="square"
      :set-all-colors-to="setAllColorsTo"
      :fdynamic-colors="fdynamicColors"
      :dynamic-colors="dynamicColors"
      v-for="(square,index) in squares"
      :key="index"
    />
	</div>

</template>

<script>
  import SquareColores from './SquareColores'

  export default  {
    name: 'src-components-container-colores',
    props: ['fmensajes',
            'mensajes',
            'fsquare',
            'squares',
            'setAllColorsTo',
            'fdynamicColors',
            'dynamicColors'
           ],
    components: {
      SquareColores
    }

  }

</script>

<style scoped lang="css">
</style>
