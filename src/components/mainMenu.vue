<template lang="">
    <div class="pdfRender">
        <div class="page">
            <createComponent
                v-for="(object, index) in objects" 
                @object-focus="$emit('object-focus', $event)"
                :key="index"
                :object=object
            ></createComponent>
        </div>
    </div>
</template>
<script>
import createComponent from './createComponent.vue';
export default {
    components: {
        createComponent
    },
    props: ['objects']
}
</script>
<style scoped>
    .pdfRender{
        width: 60%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    .page{
        aspect-ratio: 1 / 1.41;
        width: 80%;
        background-color: white;
        padding: 10px;
        align-content: stretch;
        display: flex;
        flex-direction: column;
        gap: 10px;
    }
</style>