<template>
    <div class="slice">
        <div class="post-wrap">
            <div class="features">

                 <div class="title-container"  v-if="!this.$route.params.slug">
                    <h1 class="title-shadow">Features</h1>
                    <h1 class="title">Features</h1>
                </div>
                <div class="post-title-wrap">
                    <transition class="post-title" v-for="(idx, i) in this.postBody" :key="i">
                      
                       <div class="slider" v-if="sortedPosts(idx.link)">
                         <div class="image" v-bind:style="idx.acf.image ? `background-image: url('${idx.acf.image.url}'); background-size: cover;'` : ``"/>

                          <a :href="idx.link.replace('https://privatesuitemag.com', '')">

                         <div class="copy">
                          <h4 v-html="idx.title.rendered"/>
                          <p v-html="idx.content.rendered.slice(0,150) + '...'"/>
                          </div>
                          </a>
                    </div>
                    </transition>
                </div>
            </div>
            </div>
  </div>
</template>

<script>

import { mapState } from 'vuex'

export default {
  name: 'Features',

  data() {

      return {
      }
  },
  methods: {
    sortedPosts(link) {
      if (link.toString().includes('features')) {
        return true;
      }
    }
  },
  //grabbing the values from wordpress, and assigning them to the variables
    computed: mapState ([
      'postBody'
    ])
}
</script>

<style lang="stylus" scoped>

@import "../stylesheets/styles.styl";
.post-title-wrap {
    margin: auto;
    display:flex;
    @media screen and (max-width:768px) {
      flex-direction:column;

      }
}
.post-wrap:nth-child(even) > .slider{
      width: calc((2 / 9) * 100%);
}
.image {
  height: 10em;
  position: relative;
  width: 10em;
  background-color: white;
  opacity: 0.5;
  width: calc((2 / 3) * 100%);
}
.slider {
    width: calc((3 / 9) * 100%);
    margin-bottom: 5em;
    
}
.news .slider {
    width: calc((5 / 9) * 100%);
}
.news .image {
    width: calc((5 / 9) * 100%);
    position: relative;
      height: 100%;
}
.title-container h1{
    font-size: 4em;
    margin-bottom: 0;
    text-align: left;
    margin-top: 0;
    -webkit-text-stroke: 1px black;
    -webkit-text-fill-color: transparent;
    
}
.title-shadow {
    position: absolute;
    padding: 3px;
    opacity: 0.3;
}
/* .title:before {
    content: 'Reviews';
    position: absolute;
    padding: 3px;
    opacity: 0.3;
} */
h4 {
  text-align: left;
}
.copy {
  margin-right: calc(((1 / 9) * 100%) * 3);
}
@media screen and (max-width:768px)
  .slider, .copy, .image
    width 100%
    margin 0
</style>
