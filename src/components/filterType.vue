<template>
    <div class="filter-type">
        <p >{{ item.name }}</p>
        <div class="img" 
        :style="{backgroundImage:'url(' + image + ')'}"
        :class='item.name'
        @click="selectFilter"></div>
    </div>
</template>
<script>
import eventBus from '../event-bus'
export default {
    props:{
        item:Object,
        image:String
    },
    methods:{
        selectFilter:function(){
            eventBus.$emit('selectedFilter',this.item.name)
        }
    }
}
</script>
<style lang="scss" src='../styles/filter-type.scss'>

</style>