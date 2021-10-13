<template>
  <!-- <div class="container"> -->
    <img id="img1" :src="data.src" />
  <!-- </div> -->
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      data: {
        src: {}
      }
    }
  },
  beforeMount(){
    this.getPhoto();
  },
  components: {

  },
  methods: {
    async getPhoto() {
      let url = 'https://images.unsplash.com/photo-1513313778780-9ae4807465f0?auto=format&fit=crop&w=634&q=80';
      // const res = await fetch('https://api.agify.io/?name=michael');
      const request = new Request(
        url, {
          method: "GET",
          mode: "cors",
          cache: "default"
        }
      );
      const res = await fetch(request);
      const imageBlob = await res.blob();
      let img = document.createElement('IMG');
      document.querySelector('#img1').appendChild(img);
      img.src = URL.createObjectURL(imageBlob);
      this.data.src = img.src;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  width:100%;
  height:100vh;
}
</style>
