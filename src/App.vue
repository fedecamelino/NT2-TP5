<template>
  <div id="App">
    <HeaderColores :dynamic-colors="dynamicColors" />

    <NavigatorColores
      :reset="reset"
      :easy="easy"
      :hard="hard"
      :restart-button="mensajes.restartButton"
      :message-display="mensajes.messageDisplay"
      :is-hard="isHard"
    />

    <ContainerColores
      :fmensajes="fmensajes"
      :mensajes="mensajes"
      :fsquare="fsquare"
      :squares="squares"
      :set-all-colors-to="setAllColorsTo"
      :fdynamic-colors="fdynamicColors"
      :dynamic-colors="dynamicColors"
    />
  </div>
</template>

<script>
  import HeaderColores from "./components/HeaderColores.vue";
  import NavigatorColores from "./components/NavigatorColores.vue";
  import ContainerColores from "./components/ContainerColores.vue";

  export default {
    name: "App",
    components: {
      HeaderColores,
      NavigatorColores,
      ContainerColores,
    },
    mounted() {
      this.init();
    },
    data() {
      return {
        dynamicColors: {
          pickedColor: "RBG",
          headerColor: "",
        },
        fdynamicColors: {
          headerColor: this.setHeaderColor,
        },
        mensajes: {
          messageDisplay: "",
          restartButton: "New colors",
        },
        fmensajes: {
          messageDisplay: this.setMessageDisplay,
          restartButton: this.setRestartButton,
        },
        fsquare: {
          backgroundColor: this.setBackgroundColor,
        },
        colorCount: {
          easy: 3,
          hard: 6,
        },
        isHard: true,
        colors: [],
        squares: [],
      };
    },

    methods: {
      setHeaderColor(color) {
        this.dynamicColors.headerColor = color;
      },

      setMessageDisplay(mensaje) {
        this.mensajes.messageDisplay = mensaje;
      },

      setRestartButton(mensaje) {
        this.mensajes.restartButton = mensaje;
      },

      setBackgroundColor(index, color) {
        this.squares[index].backgroundColor = color;
      },

      reset() {
        this.restart();
      },

      easy() {
        if (this.isHard) {
          this.isHard = false;
          for (let i = 0; i < this.colorCount.easy; i++) {
            let anulable = this.colorCount.easy + i;
            this.squares[anulable].display = "none";
          }
          this.restart();
        }
      },

      hard() {
        if (!this.isHard) {
          this.isHard = true;
          this.restart();
          for (let i = 3; i < this.colorCount.hard; i++) {
            this.squares[i].display = "block";
          }
        }
      },

      init() {
        for (let i = 0; i < this.colorCount.hard; i++) {
          this.squares.push({
            display: "block",
            backgroundColor: "",
          });
        }
        this.restart();
      },

      PickColor() {
        let elementos;
        if (this.isHard) {
          elementos = 6;
        } else {
          elementos = 3;
        }
        return Math.floor(Math.random() * elementos);
      },

      createNewColors(numbers) {
        var array = [];
        for (var i = 0; i < numbers; i++) {
          array.push(this.createRandomStringColor());
        }
        return array;
      },

      setAllColorsTo(color) {
        this.squares.forEach((square) => {
          square.backgroundColor = color;
        });
      },

      createRandomStringColor() {
        var newColor =
          "rgb(" +
          this.randomInt() +
          ", " +
          this.randomInt() +
          ", " +
          this.randomInt() +
          ")";
        return newColor;
      },

      randomInt() {
        return Math.floor(Math.random() * 256);
      },

      restart() {
        this.colors = this.createNewColors(this.colorCount.hard);
        this.dynamicColors.pickedColor = this.colors[this.PickColor()];
        this.dynamicColors.headerColor = "steelblue";
        this.mensajes.messageDisplay = "";
        this.mensajes.restartButton = "New Colors!";
        for (let i = 0; i < this.squares.length; i++) {
          this.squares[i].backgroundColor = this.colors[i];
        }
      },
    },
  };
</script>

<style>
  pre {
    color: white;
  }

  body {
    background: #232323;
    margin: 0;
    font-family: "Montserrat", "Avenir";
  }

  h1 {
    font-weight: normal;
    line-height: 1.1;
    padding: 20px 0;
  }

  #navigator {
    background: #ffffff;
    height: 30px;
    text-align: center;
    margin: 0;
    margin-top: -30px;
  }

  #header {
    transition: all 0.3s;
    background: steelblue;
    text-transform: uppercase;
    text-align: center;
    margin: 0;
    color: white;
  }

  #colorDisplay {
    font-size: 200%;
  }

  .square {
    width: 30%;
    background: blue;
    padding-bottom: 30%;
    float: left;
    margin: 1.66%;
    border-radius: 10%;
    transition: background 0.8s;
    -webkit-transition: background 0.8s;
    -moz-transition: background 0.8s;
  }

  #container {
    margin: 20px auto;
    max-width: 600px;
  }

  #message {
    color: #000000;
    display: inline-block;
    width: 20%;
  }

  .selected {
    background-color: steelblue;
    color: white;
  }

  button {
    border: none;
    background-color: white;
    font-family: "Montserrat", "Avenir";
    text-transform: uppercase;
    height: 100%;
    font-weight: 700;
    letter-spacing: 1px;
    color: steelblue;
    transition: all 0.3s;
    outline: none;
  }

  button:hover {
    color: white;
    background-color: steelblue;
  }
</style>
