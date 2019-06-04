<template>
  <div id="app">
    <div class="app-phone">
      <div class="phone-header">
        <a v-if="step===2 || step ===3" 
          class="cancel-cta"
          @click='toHome'>Cancel</a>
        <img src="./assets/vue_gram_logo_cp.png" alt="">
        <a v-if="step===2" class="next-cta" @click='step++'>Next</a>
        <a v-if="step===3" class="next-cta" @click='share'>Share</a>
      </div>
      <phoneBody 
        :posts='posts'
        :step='step'
        :image='image'
        :filters='filters'
        :selectItem='selectItem'
        v-model='caption'></phoneBody>
      <div class="phone-footer">
        <div class="home-cta">
          <i class="fas fa-home fa-lg" @click='toHome'></i>
        </div>
        <div class="upload-cta">
          <input type="file" name="file" id="file" @change="uploadImage" :disabled='step !==1' ref='demo'>
          <label for="file">
            <i class="far fa-plus-square fa-lg"></i>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script >
import phoneBody from './components/phoneBody'
import posts from './data/posts'
import filters from './data/filters'
import eventbus from './event-bus'

export default {
  name: 'app',
  components:{
    phoneBody:phoneBody
  },
  created(){
    eventbus.$on('selectedFilter', filter=>{
      this.selectItem = filter
    })
  },
  data(){
    return {
      posts,
      filters,
      step:1,
      image:'',
      selectItem:'',
      caption:'',
      fileLength:[]
    }
  },
  methods:{
    uploadImage:function(e){
      const files = e.target.files;
      if(!files.length) return
      const reader = new FileReader();
      reader.readAsDataURL(files[0]);
      reader.onload = e =>{
        this.image = e.target.result;
        this.step = 2;
      }
    },
    toHome:function(){
      this.image = '';
      this.selectItem = '';
      this.$refs.demo.value = ''
      this.step = 1;
    },
    share(){
      const post = {
        username: "suyiyi",
        userImage:"https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/pug_personal.jpg",
        postImage:this.image,
        likes: 0,
        hasBeenLiked: false,
        caption: this.caption,
        filter: this.selectItem
      }
      this.posts.unshift(post);
      this.toHome();
      this.$refs.demo.value = ''
    }
  }
  
}
</script>

<style lang="scss" src='./styles/app.scss'>

</style>
