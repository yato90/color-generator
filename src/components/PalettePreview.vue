<template>
    <div class="palette_preview">
      <div
        v-for="(color, index) in palette"
        :key="index"
        class="color_swatch"
        :style="{ backgroundColor: color }"
        @click="copyColor(color)"
      >
        {{ color }}
        <div v-if="copy" class="message">Код скопирован</div>
      </div>
    </div>
</template>
  
<script>
  export default {
    props: {
      palette: Array,
    },
    data() {
      return {
        copy: false,
      };
    },
    methods: {
      copyColor(color) {
        const input = document.createElement('input');
        input.value = color;
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
.palette_preview {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 20px;
}

.color_swatch {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 80px;
    height: 80px;
    margin: 5px;
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s ease;
    position: relative;
}

.color_swatch:hover {
    background-color: rgba(0, 0, 0, 0.1);
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
    z-index: 1;
    display: none;
}

.color_swatch:hover .message {
    display: block;
}
</style>