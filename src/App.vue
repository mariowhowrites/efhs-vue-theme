<template>
  <div class="container">
  <div class="wrapper">
    <div class="first row">
      <img class="col-xs-4 col-xs-offset-4 col-md-4 col-md-offset-4 logo" src="./assets/logo.png">
    </div>
    <div class="second row">
      <h1></h1>
      <h2>EcoFriendly Hospitality Solutions</h2>
      <ul>
        <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
        <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
        <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
        <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      </ul>
    </div>
    <div class="third row">
      <h2>Ecosystem</h2>
      <ul>
        <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
        <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
        <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      </ul>
    </div>
  </div>
  <div class="second">
    <h2>Highlighting the great beyond</h2>
    <p>Huh! Wow!</p>
    <button @click="axiosTest()">button</button>
  </div>
  </div>
</template>

<script>
  import EfhsHeader from './EfhsHeader.vue';
  export default {
    name: 'app',
    data () {
      return {
          msg: 'Welcome to Your Vue.js App'
      }
    },
      components: {
        'efhs-header': EfhsHeader
      },
      methods: {
        axiosTest () {
            axios.get('https://teamtreehouse.com/mariovega3.json')
                .then( (res) => { console.log(res.data); })
                .catch( (err)  =>  { console.log(err);  } );
        }
      }
}
</script>

<style lang="scss">
  .wrapper {
    font-family: 'Roboto Slab', 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /*margin-top: 60px;*/
    height: 100vh;
    background: whitesmoke;
  }

  .second {
    text-align: center;
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
