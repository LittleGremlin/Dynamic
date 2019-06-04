<template>
    <div class="vuegram-post">
        <div class="header level">
            <div class="level-left">
                <figure class="image is-32x32">
                    <img :src="item.userImage" alt="">
                </figure>
                <span class="username">{{ item.username }}</span>
            </div>
        </div>
        <div class="image-container"
                :class='item.filter'
                :style="{backgroundImage:'url(' + item.postImage + ')'}"
                @dblclick="clicklike">
        </div>
        <div class="content">
            <div class="heart">
                <i class="far fa-heart" @click="clicklike" :class='{fas:item.hasBeenLiked}'></i>
            </div>
            <p class="likes">{{ item.likes }} likes</p>
            <p class="caption">
                <span>{{ item.username }}</span></p>
                {{ item.caption }}
        </div>
    </div>
</template>
<script>
export default {
    props:{
        item:Object
    },
    methods:{
        clicklike:function(){
            console.log(this.item)
            this.item.hasBeenLiked ? this.item.likes-- : this.item.likes++;
            this.item.hasBeenLiked = !this.item.hasBeenLiked;

        }
    }
}
</script>
<style lang="scss" src='../styles/vuegram-post.scss'>

</style>


