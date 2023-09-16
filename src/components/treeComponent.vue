<template lang="">
    <ul>
        <li v-for="(object, index) in objects" :key="index">
            <div class="section">
                <div
                    class="arrow"
                    v-if="isSection(object.childrens)"
                    @click="showOrHideChildrens"
                >
                    <span class="material-symbols-outlined" v-show="childrenShow">
                        arrow_drop_down
                    </span>
                    <span class="material-symbols-outlined" v-show="!childrenShow">
                        arrow_right
                    </span>
                </div>
                <div>
                    {{object.name}} || {{object.type}}
                </div>
                <div class="options">
                    <span class="material-symbols-outlined danger" @click="removeObject(index)">
                        delete
                    </span>
                    <span class="material-symbols-outlined" @click="addObject(index)">
                        add
                    </span>
                </div>
            </div>
            <treeComponent
                v-show="childrenShow"
                v-if="isSection(object.childrens)"
                @remove-item="passObject"
                @add-item="passObject"
                :objects=object.childrens
                :upperIndex=index
                :key=index
            ></treeComponent>
        </li>
    </ul>
</template>
<script>
export default {
    props: ['objects', 'upperIndex'],
    data() {
        return {
            childrenShow: true
        }
    },
    methods: {
        isSection(object){
            return object && object.length;
        },
        showOrHideChildrens(){
            this.childrenShow = !this.childrenShow;
        },
        removeObject(index){
            this.objects.splice(index, 1);
            this.$emit('remove-item', {upperIndex: this.upperIndex, childrens: this.objects})
        },
        passObject(object){
            this.objects[object.upperIndex].childrens = object.childrens;
            this.$emit('remove-item', {upperIndex: this.upperIndex, childrens: this.objects})
        },
        addObject(index){
            this.objects.splice(index+1, 0, {name: 'new '+index});
            this.$emit('add-item', {upperIndex: this.upperIndex, childrens: this.objects})
        }
    }
}
</script>
<style scoped>
    ul{
        padding-left: 20px;
        list-style-type: none;
    }
    li>ul{
        border-left: 1px solid var(--text-color);
        margin-left: 12px;
    }
    .section{
        display: flex;
        flex-direction: row;
    }
    .section:hover .options{
        opacity: 1;
        transition: .5s opacity;
    }
    .arrow:hover{
        cursor: pointer;
    }
    .options{
        opacity: 0;
    }

    .options > span:hover{
        cursor: pointer;
    }
</style>