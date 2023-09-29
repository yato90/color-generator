<template>
  <div id="main">
      <header>
        <h1>Генератор цветовой палитры</h1>
      </header>
      <main>
        <color-picker @color-selected="addColor" />
        <palette-preview :palette="palette" />
        <button @click="generatePalette">Сгенерироваать палитру</button>
      </main>
  </div>
</template>

<script>
import ColorPicker from './components/ColorPicker.vue';
import PalettePreview from './components/PalettePreview.vue';

export default{
  components:{
    ColorPicker,
    PalettePreview,
  },
  data(){
    return{
      colors:[],
      palette:[],
      copiedMessage: null,
    };
  },
  methods:{
    addColor(color) {
      this.colors.push(color);
    },
    generatePalette() {
      this.palette = [...this.colors];
    },
  }
};
</script>

<style scoped>
body {
  font-family: 'Helvetica Neue', sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #ffffff;
}
#main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #ffffff;
  color: #000000;
}
header {
  text-align: center;
  padding: 10px 0;
  margin-bottom: 20px;
}
h1 {
  margin: 0;
  font-size: 24px;
}
main {
  background-color: #1a1a1a;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  background-color: #0868cf;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin-top: 10px;
  cursor: pointer;
  border-radius: 5px;
  margin-left: 5px;
}

button:hover {
  background-color: #0056b3;
}
.message {
  background-color: rgba(0, 0, 0, 0.7);
  color: #fff;
  padding: 5px 10px;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1000;
}
</style>
