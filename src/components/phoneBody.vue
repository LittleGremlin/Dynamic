<template>
    <div class="phone-body">
        <!-- {{ posts }} -->
        <div class="feed" v-if='step===1' v-dragscroll>
            <VuegramPost 
                v-for='(item,index) in posts' 
                :key='index' 
                :item='item'></VuegramPost>
        </div>
        <div v-if="step===2">
            <div class="selected-image"
            :style="{backgroundImage:'url(' + image + ')'}"
            :class='selectItem'></div>
            <div class="filter-container" v-dragscroll>
                <Filtertype 
                :image='image' 
                v-for="(item,index) in filters" 
                :key='index'
                :item='item'></Filtertype>
            </div>
        </div>
        <div v-if="step===3">
            <div class="selected-image"
            :style="{backgroundImage:'url(' + image + ')'}"
            :class='selectItem'></div>
            <div class="caption-container">
                <textarea placeholder="Write a caption"
                :value='value'
                @input='inputText'></textarea>
            </div>
        </div>

    </div>
</template>
<script>
import VuegramPost from './VuegramPost'
import Filtertype from './filterType'
export default {
    props:{
        posts:Array,
        step:Number,
        image:String,
        filters:Array,
        selectItem:String,
        value:String
    },
    components:{
        VuegramPost:VuegramPost,
        Filtertype:Filtertype
    },
    methods:{
        inputText(e){
            this.$emit('input',e.target.value)
        }
    }
}
</script>
<style lang="scss" src='../styles/phone-body.scss'>

</style>


