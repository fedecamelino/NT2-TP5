<template>

  <div :style="square" @click="squareClick()"></div>

</template>

<script>

  export default  {
    name: 'src-components-square-colores',
    props: ['index',
            'fmensajes',
            'mensajes',
            'fsquare',
            'square',
            'setAllColorsTo',
            'fdynamicColors',
            'dynamicColors'
           ],
    methods: {
      squareClick() {
        let clickedColor = this.square.backgroundColor;

        if (clickedColor === this.dynamicColors.pickedColor) {
          this.fmensajes.messageDisplay("You Picked Right!");
          this.setAllColorsTo(this.dynamicColors.pickedColor);
          this.fmensajes.restartButton("Play Again!");
          this.fdynamicColors.headerColor(this.dynamicColors.pickedColor);
        } 
        else {
          this.fsquare.backgroundColor(this.index, "#232323");
          this.fmensajes.messageDisplay("Try Again!");
        }
		  }
    }
  }

</script>

<style scoped lang="css">
</style>
