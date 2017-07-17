<template>
<div id="app">
  <h1>Generate a QR code with your image!</h1>

  <h2>Select an image</h2>
  <button><label for="image">Select</label></button>
  <input type="file" id="image" @change="onFileChange">

  <h2>Enter URL</h2>
  <input type="text" v-model="config.value">

  <div id="qart">
    <vue-q-art :config="config" :downloadButton="downloadButton"></vue-q-art>
  </div>
</div>
</template>

<script>
import VueQArt from '../src/vue-qart.vue'
export default {
  components: {
    VueQArt
  },
  name: 'app',
  data() {
    return {
      config: {
        value: 'https://www.instagram.com/p/BWfHL4OFUMC/',
        imagePath: './assets/kit.jpg',
        filter: 'color',
        size: 500
      },
      downloadButton: true
    }
  },
  methods: {
    onFileChange(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(files[0]);
    },
    createImage(file) {
      var reader = new FileReader();
      var vm = this;

      reader.onload = (e) => {
        vm.config["imagePath"] = e.target.result;

        // update the image by changing "value"
        vm.config["value"] += ' ';
      };
      reader.readAsDataURL(file);
    },
  }
}
</script>

<style>
#app {
  padding: 0;
  margin: 0 auto;
  width: 750px;
  color: #2c3e50;
  font-size: 20px;
  text-align: center;
  font-family: Times;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#qart {
  margin: 50px;
}

h1, h2 {
  font-weight: normal;
  margin: 30px 0 10px;
}

input[type="file"] {
  display: none;
}

@media screen and (max-width: 479px) {
  #app {
    padding: 0;
    margin: 0 auto;
    width: 100%;
  }
}
</style>
