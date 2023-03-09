<template>
  <div style="width: 100%;">
    <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">EXPRESS.JS + VUE.JS</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarCollapse"
          aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
          <ul class="navbar-nav me-auto mb-2 mb-md-0">
            <li class="nav-item">
              <router-link :to="{name: 'home'}" class="nav-link" aria-current="page">HOME</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{name: 'posts.index'}" class="nav-link">POSTS</router-link>
            </li>
            <li class="nav-item">
              <router-link :to="{name: 'posts.create'}" class="nav-link">CREATE</router-link>
            </li>
          </ul>
          <div class="d-flex">
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
            <button class="btn btn-success" type="submit">Search</button>
          </div>
        </div>
      </div>
    </nav>

    <!-- render vue router -->
    <router-view></router-view>
  </div>
  
  <div style=" max-width: 400px; margin-top: 20px;">
    <HeaderWeb @changeTitle="ubahText" :text="textHeader" />
    <img alt="Vue logo" src="./assets/logo.png">
    <h2>Nama: {{ nama }}</h2>
    <input class="form-control" type="text" v-model="nama">
    <button class="btn btn-primary w-100 mt-2" @click="changeName">Detail</button>
    <h2><a :href="url" target="_blank">Menuju CV Saya</a></h2>
    <input class="form-control" type="text" v-model="cari" placeholder="Cari...">
    <div v-if="products.length" style="display: flex; justify-content: center; margin-top: 10px; text-align: start;">
      <table class="table">
        <thead>
          <tr>
            <th>Nama Product</th>
            <th>Harga</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in cariData" :key="item.id">
            <td>{{ item.title }}</td>
            <td>{{ item.price }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else>
      <p>Data Not Found</p>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import HeaderWeb from '@/components/HeaderWeb.vue'

export default {
  name: 'App',
  components: {
    HeaderWeb,
    // HelloWorld
  },
  data() {
    return {
      nama: 'M Yusril Aprial',
      url: 'https://cv-myusrila.vercel.app/',
      cari: "",
      products: [],
      textHeader: "Ini Adalah Header",
    }
  },
  methods: {
    changeName() {
      this.nama = `${this.nama} (D3 Manajemen Informatika)`;
    },
    ubahText(newText){
      this.textHeader = newText;
    },
  },
  beforeCreate() {
    console.log('beforeCreate');
  },
  created() {
    console.log('created');
    this.products = [
      {id: 1, title: 'Komputer', price: 100},
      {id: 2, title: 'Mouse', price: 200},
      {id: 3, title: 'Headset', price: 300},
      {id: 4, title: 'Keyboard', price: 400},
    ];
  },
  beforeMount() {
    console.log('beforeMount');
  },
  mounted() {
    console.log('mounted');
  },
  computed: {
    cariData(){
      return this.products.filter((item)=>{
        return item.title.toLowerCase().includes(this.cari.toLowerCase());
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
.mt-custom {
  margin-top: 110px;
}
</style>
