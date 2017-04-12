<template>
  <div class="container-fluid">
    <div class="wrapper">
      <div class="first row">
          <div class="col-xs-12" style="height: 700px;"><img class="logo" style="height: inherit;" src="./assets/EFHS_symbol_color.png"></div>
      </div>
      <div class="row">
        <h1></h1>
        <h2 class="col-xs-12">EcoFriendly Hospitality Solutions</h2>
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
        <div class="col-xs-12">
            <div class="row">
              <div class="col-xs-6">
                <div class="row">
                  <section class="col-xs-12">
                      <div class="featured-wrap">
                          <h1>EcoLastic Foam Cushions</h1>
                          <p>Hello! This is some text describing EcoLastic Foam Cushions.</p>
                      </div>
                  </section>
                </div>
              </div>
              <div class="col-xs-6">
                  <div style="overflow: hidden; max-height: 600px;"><img :src="postImages[0]" alt=""/></div>
                <div class="col-xs-12"><button @click="getImage(posts[0])">Wow!!!</button></div>
              </div>
            </div>
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
                postImages: [],

            }
        },
        components: {
            'efhs-header': EfhsHeader
        },
        methods: {
            getPosts () {
                axios.get('https://ecofriendlyhospitalitysolutions.com/wp-json/wp/v2/posts/?_embed')
                    .then( res => {
                        for ( let post of res.data ) {
                            this.posts.push(post)
                        }
                    })
                    .catch( err => { console.log(err); } );
            },
            showPosts () {
                console.log(this.posts);
                for ( let post of this.posts ) {
                    console.log( post.featured_media );
                }
            },
            getImage (post) {
                const imageID = post.featured_media;
                axios.get('https://ecofriendlyhospitalitysolutions.com/wp-json/wp/v2/media/' + imageID + '/')
                    .then( res => {
                        console.log(res);
                        this.postImages.push( res.data.source_url );
                        console.log(this.postImages);
                    })
                    .catch( err => { console.log(err) })
            },
        },
        created () {
            this.getPosts();
            this.showPosts();
        }
    }
</script>

<style lang="scss">
  body {
    background: whitesmoke;
  }
  .wrapper {
    font-family: 'jaf-domus-titling-web', 'Roboto Slab', 'Avenir', Helvetica, Arial, sans-serif;
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
      font-family: 'jaf-domus-titling-web', sans-serif;
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
    p {
        font-family: "mrs-eaves-roman-lining", serif;
    }

    .featured-wrap {
        background: blue;
        color: white;
    }
</style>
