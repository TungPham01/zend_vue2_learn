
<template>
  <div id="app">
    <button 
      @click="title = 'xin chào duy tùng'"
    >Thay đổi title từ component app.vue</button>
    <HeaderComponent 
      v-bind:title="title" 
      @changeTitleEvent="handleChangeTitle"
    />
    <ListUser
      @deleteUser="handleDeleteUser"
    />
    <RefComponent />
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
import HeaderComponent from './Components/HeaderComponent'
import ListUser from './Components/ListUserComponent'
import RefComponent from './Components/RefComponent'
export default {
  name: 'app',
  data () {
    return {
      title: 'Welcome to Your Vue.js App',
    }
  }, 
  components: {
    HeaderComponent,
    ListUser,
    RefComponent
  },
  methods: {
    handleChangeTitle (data) {
      this.title = data.title
      console.log('handleChangeTitle App.vue')
    },
    handleDeleteUser (data) {
      console.log('handleDeleteUser App.vue', data)
    }
  },
  beforeCreate() {
    console.log('beforeCreate', this.title)
  },
  created() {
    console.log('created', this.title)
  },
  beforeMount() {
    console.log('beforeMount', this.title)
  },
  mounted() {
    console.log('mounted', this.title)
  },
  beforeDestroy() {
    console.log('beforeDestroy')
  },
  destroyed() {
    console.log('destroyed')
  }


}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
