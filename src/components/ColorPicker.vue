<template>
    <div class="color_picker">
        <input type="color" v-model="selectedColor" @input="updatePalette" />
        <button @click="copyColor">Копировать</button>
        <div v-if="copy" class="message">Цвет скопирован</div>
    </div>
</template>

<script>
export default{
    data(){
        return{
            selectedColor:'#ffffff',
            copy: false,
        };
    },
    methods: {
        updatePalette(){
            this.$emit('color-selected', this.selectedColor);
        },
        copyColor(){
            const input = document.createElement('input');
            input.value = this.selectedColor;
            document.body.appendChild(input);
            input.select();
            document.execCommand('copy');
            document.body.removeChild(input);
    
            this.copy = true;
            setTimeout(() => {this.copy = false;}, 1000);
        },
    },
};
</script>


<style scoped>
.color_picker {
    display: flex;
    align-items: center;
    margin: 15px;
  }
  
  .color_picker button {
    background-color: #0868cf;
    color: #fff;
    border: none;
    padding: 5px 10px;
    margin-left: 5px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  
  .color_picker button:hover {
    background-color: #0056b3;
  }
  
  .message {
    background-color: rgba(0, 0, 0, 0.7);
    color: #fff;
    padding: 5px 10px;
    border-radius: 5px;
    position: absolute;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1000;
  }
</style>
