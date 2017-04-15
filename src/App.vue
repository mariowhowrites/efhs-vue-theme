<template>
  <div class="container-fluid">
    <efhs-header></efhs-header>
    <div v-for="post in posts">
      <vendor-component
            :post="post">
      </vendor-component>
    </div>
  </div>
</template>

<script>
    import EfhsHeader from './EfhsHeader.vue';
    import VendorComponent from './VendorComponent.vue';

    export default {
        name: 'app',
        data () {
            return {
                restURL: 'https://ecofriendlyhospitality.solutions/wp-json/wp/v2/',
                posts: [],
                postImages: [],
            }
        },
        components: {
            'efhs-header': EfhsHeader,
            'vendor-component': VendorComponent
        },
        methods: {
            /*
            * fetch the posts from WP. Should only be used if no LocalStorage exists.
            *
             */
            fetchPosts () {
                localStorage.removeItem( 'posts' );
                axios.get( this.restURL + 'posts')
                    .then( res => {
                        for ( let post of res.data ) {
                            this.getImage( post );
                        }
                        localStorage.setItem( 'posts', JSON.stringify( this.posts ) );
                    })
                    .catch( err => { console.log(err); } );
            },
            getImage (post) {
                const imageID = post.featured_media;
                if ( !imageID ) {
                    //console.log( 'The post '+ post.title.rendered +' has no featured image.');
                    this.posts.push( post );
                    return;
                }
                else {
                    axios.get(this.restURL + 'media/' + imageID + '/')
                        .then(res => {
                            post.featured_image_details = res.data;
                            this.posts.push( post );
                        })
                        .catch(err => {
                            console.log(err)
                        })
                }
            },
        },
        created () {
            this.fetchPosts();
            console.log( JSON.parse( localStorage.getItem( 'posts' ) ) );

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
</style>
