<template >
    <div class="main" v-show="type == 'text'">
        <div>
            <h3>Aligments</h3>
            <br>
            <div class="blocks">
                <div class="block">
                    <span class="material-symbols-outlined">
                        format_align_left
                    </span>
                    <p>Align left</p>
                </div>
                <div class="block">
                    <span class="material-symbols-outlined">
                        format_align_center
                    </span>
                    <p>Align center</p>
                </div>
                <div class="block">
                    <span class="material-symbols-outlined">
                        format_align_right
                    </span>
                    <p>Align right</p>
                </div>
            </div>
        </div>
    </div>
    <div class="main" v-show="type == 'section'">
        <div>
            <h3>Direction</h3>
            <br>
            <div class="blocks">
                <div class="block" @click="changeClass('flex-column')">
                    <span class="material-symbols-outlined">
                        flex_direction
                    </span>
                    <p>Column</p>
                </div>
                <div class="block" @click="changeClass('flex-row')">
                    <span class="material-symbols-outlined" style="transform: rotate(-90deg);">
                        flex_direction
                    </span>
                    <p>Row</p>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: ['type','object'],
    data() {
        return {
            flex: ['flex-column', 'flex-row']
        }
    },
    methods: {
        changeClass(classText){
            if(this.object.class && this.object.class.length){
                let index = this.searchIfInArray(classText.split('-')[0]);
                if(index != false){
                    this.object.class.split(index, 1, classText);
                }else{
                    this.object.class.push(classText);
                }
            }else{
                this.object.class = new Array(classText);
            }
        },

        searchIfInArray(prefix){
            for(let item of this[prefix]){
                let indexOfItem = this.object.class.indexOf(item);
                if(indexOfItem > -1) return indexOfItem;
            }
            return false;
        }
    },
}
</script>
<style>
    .main{
        display: flex;
        flex-direction: column;
        gap: 20px;
        padding: 10px;
    }
    .blocks{
        display: flex;
        flex-direction: row;
        gap: 20px;
        justify-content: space-evenly;
    }
    .block{
        text-align: center;
        font-size: 12px;
        border-radius: 8px;
        padding: 10px;
        min-height: 64px;
        min-width: 56px;
    }
    .block:hover{
        background-color: #F7F8F8;
        cursor: pointer;
    }
</style>