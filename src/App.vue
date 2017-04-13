<template>
  <div class="container-fluid">
    <efhs-header></efhs-header>
    <div class="row" style="text-align: center; height: 100vh;">
        <div class="col-xs-12">
            <div class="row">
              <div class="col-xs-6 featured-wrap">
                <div class="row">
                  <section class="col-xs-12">
                      <h1>EcoLastic Foam Cushions</h1>
                      <p>Hello! This is some text describing EcoLastic Foam Cushions.</p>
                  </section>
                </div>
              </div>
              <div class="col-xs-6">
                  <div style="overflow: hidden; height: inherit;"><img :src="postImages[0]" alt=""/></div>
                <div class="col-xs-12"><button @click="getImage(posts[0])">Wow!!!</button></div>
              </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
    import EfhsHeader from './EfhsHeader.vue';
    import EfhsVendor from './EfhsVendor.vue';
    export default {
        name: 'app',
        data () {
            return {
                posts: [],
                postImages: [],
            }
        },
        components: {
            'efhs-header': EfhsHeader,
            'efhs-vendor': EfhsVendor
        },
        methods: {

            /*
            * fetch the posts from WP. Should only be used if no LocalStorage exists.
            *
             */
            fetchPosts () {
                axios.get('https://ecofriendlyhospitalitysolutions.com/wp-json/wp/v2/posts/')
                    .then( res => {
                        for ( let post of res.data ) {
                            this.posts.push(post);
                            this.getImage(post);
                        }

                        localStorage.setItem( 'posts', JSON.stringify( this.posts ) );
                        console.log( this.posts );
                    })
                    .catch( err => { console.log(err); } );
            },
            showPosts () {
                //console.log(this.posts);
                for ( let post of this.posts ) {
                    //console.log( post.featured_media );
                }
            },
            getImage (post) {
                const imageID = post.featured_media;
                axios.get('https://ecofriendlyhospitalitysolutions.com/wp-json/wp/v2/media/' + imageID + '/')
                    .then( res => {
                        //console.log(res);
                        this.postImages.push( res.data.source_url );
                        //console.log(this.postImages);
                    })
                    .catch( err => { console.log(err) })
            },
        },
        created () {
            this.getPosts();
            this.showPosts();
        },
    }
</script>

<style lang="scss">
  body {
    background: whitesmoke;
    font-family: "mrs-eaves-roman-lining", serif;
  }
  .wrapper {
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

  h1, h2, h3, h4, h5, h6 {
    font-family: 'jaf-domus-titling-web', Helvetica, Arial, sans-serif;
  }
  h1, h2 {
      font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
    font-family: 'jaf-domus-titling-web', sans-serif;
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
        background: #18B9E7;
        color: white;
    }
</style>
