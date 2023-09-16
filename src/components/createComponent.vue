<template lang="">
    <div v-show="object.type == 'section'" :class="{focus: this.object.focus}, [this.object.class]" class="section component" @click.stop="objectFocused">
        <createComponent
            v-if="object.childrens && object.childrens.length > 0"
            v-for="(object, index) in object.childrens"
            @object-focus="$emit('object-focus', $event)"
            :key="index"
            :object=object
        ></createComponent>
    </div>
</template>
<script>
export default {
    props: ['object'],
    methods: {
        objectFocused(){
            this.object.focus = true;
            this.$emit('object-focus', this.object);
        }
    },
}
</script>
<style scoped>
    .section{
        display: flex;
        padding: 10px;
    }
    .focus{
        outline: 1px solid var(--accent-color);
    }
    .component:hover{
        outline: 1px solid var(--accent-color);
    }
</style>