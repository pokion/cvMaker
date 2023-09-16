<template lang="">
    <div>
        <p>Section tree</p>
        <treeComponent :objects="objects" @remove-item="changeObject" @add-item="changeObject"></treeComponent>
    </div>
</template>
<script>
import treeComponent from './treeComponent.vue';
export default {
    components: {
        treeComponent
    },
    props: ['objects'],
    methods: {
        changeObject(object){
            console.log(object)
            this.objects = object.childrens;
            this.$emit('tree-objects', this.objects);
        }
    },
}
</script>
<style scoped>
    
</style>