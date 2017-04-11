<template>
  <div class="container">
  <div class="wrapper">
    <div class="first row">
      <img class="col-xs-4 col-xs-offset-4 col-md-4 col-md-offset-4 logo" src="./assets/logo.png">
    </div>
    <div class="row">
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
      <p><div class="_form_1"></div></p>
      <ul>
        <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
        <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
        <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      </ul>
    </div>
  </div>
  <div class="row" style="text-align: center">
    <div class="col-xs-6">
      <div class="row">
        <div class="col-xs-10 col-xs-offset-1">
          <h1>EcoLastic Foam Cushions</h1>
        </div>
      </div>
    </div>
    <div class="col-xs-6">
      <div class="col-xs-12"><button @click="showPosts()">Wow!!!</button></div>
    </div>
  </div>
  </div>
</template>

<script>
  import EfhsHeader from './EfhsHeader.vue';
  export default {
    name: 'app',
    data () {
      return {
          posts: [],

      }
    },
      components: {
        'efhs-header': EfhsHeader
      },
      methods: {
        axiosTest () {
            axios.get('https://ecofriendlyhospitalitysolutions.com/wp-json/wp/v2/posts/')
                .then( res => {
                    for ( let post of res.data ) {
                      this.posts.push(post)
                    }
                })
                .catch( (err)  =>  { console.log(err);  } );
        },
          showPosts () {
            console.log(this.posts);
          }
      },
      created () {
        this.axiosTest();
      }
}
</script>

<style lang="scss">
  body {
    background: whitesmoke;
  }
  .wrapper {
    font-family: 'Roboto Slab', 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    height: 100vh;
  }

  .second {
    background: red;
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
