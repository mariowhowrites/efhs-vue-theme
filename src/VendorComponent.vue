<template>
    <div class="row vendor-wrapper comp-height">
        <div class="col-xs-12">
            <div class="row">
                <div class="col-xs-6">
                    <div class="row featured-wrap comp-height">
                        <section style="margin-top: 35%" class="col-xs-12">
                            <h1 v-html="post.title.rendered"></h1>
                            <div v-html="post.content.rendered"></div>
                        </section>
                    </div>
                </div>
                <div class="col-xs-6 comp-height">
                    <div style="overflow: hidden; height: inherit;"><img :src="imgMed" alt=""/></div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        props: {
            post: Object,
            //postImages: Object,
        },
        computed: {
            imgMed () {
                return this.post.featured_image_details ? this.post.featured_image_details.media_details.sizes.medium.source_url : "Hello"
            },
        },
        methods: {
            checkImg () {
                console.log(this.imgMed);
            }
        }
    }
</script>
<style scoped>
    .vendor-wrapper {
        text-align: center;
        margin-bottom: 20px;
    }
    .featured-wrap {
        background: #18B9E7;
        color: white;
    }
    .comp-height {
        height: 80vh;
       }
</style>