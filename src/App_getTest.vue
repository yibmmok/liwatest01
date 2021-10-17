<template>
    <form @submit.prevent="createPost">
      <div class="edBox">
        <input type="text" placeholder="name" v-model="post.text">
      </div>
      <div class="edBox">
        <input type="text" placeholder="title" v-model="post.day">
      </div>
      <div class="edBox">
        <input type="checkbox" placeholder="title" v-model="post.reminder">
      </div>      
      <br />
      <button type="submit">新增</button>
    </form>
    {{data}}
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      post: {},
      data: {}
    }
  },
  methods: {
    async createPost() {
      // let url = 'https://jsonplaceholder.typicode.com/posts';
      let url = 'http://localhost/api/test01/vue03_add.php';
      const esc = encodeURIComponent;
      const params = this.post;
      const query = Object.keys(params).map(k => `${esc(k)}=${esc(params[k])}`).join('&');
      const request = new Request (
        url+'?'+query, {
          method: "GET",
          mode: "cors",
          cache: "default"
          // body: JSON.stringify(this.post)
        }
      );

      const res = await fetch(request);
      const data = await res.json();
      this.data = data;
    }
    
/*  async getPhoto() {
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
    }  */
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

.edBox {
  width: 100%;
  height: 40px;
}

input {
  margin: 0 auto;
  width:250px;
  line-height:25px;
  font-size:1rem;
}
</style>
