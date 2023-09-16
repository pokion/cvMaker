<script >
	import leftMenu from './components/leftMenu.vue';
	import mainMenu from './components/mainMenu.vue';
	import rightMenu from './components/rightMenu.vue';
	export default {
    components: {
        leftMenu,
		mainMenu,
		rightMenu
    },
    data() {
        return {
            objects: [
                {name: 'john', type: 'section'},
                {name: 'pan', type: 'section'},
                {name: 'asd', type: 'section',  childrens: [{name: 'john2', type: 'section'},
                {name: 'pan2', type: 'section', childrens: [{name: 'john3', type: 'section'},
                {name: 'pan3', type: 'section', childrens: [{name: 'makamaka', type: 'section'},
                {name: 'pan2', type: 'section'},]},]},]},
                {name: 'jack', type: 'section'}
            ],
			optionType: 'section',
			referenceToObject: null
        }
    },
    methods: {
        changeObject(object){
            this.objects = object.childrens;
        },
		setReference(object){
			if(this.referenceToObject != null) this.referenceToObject.focus = false;
			this.referenceToObject = object;
		}
    },
}
</script>

<template>
	<div class="sideMenu">
		<leftMenu
			:type="optionType"
			:object="referenceToObject"
		/>
	</div>
	<div class="mainMenu">
		<mainMenu
			:objects="objects"
			@object-focus="setReference"
		/>
	</div>
	<div class="sideMenu">
		<rightMenu
			@tree-objects="changeObject"
			:objects="objects"
		/>
	</div>
</template>

<style scoped>
	.sideMenu{
		width: 20%;
		height: 100vh;
	}
	.mainMenu{
		background-color: var(--main-color-bg);
		width: 60%;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		border-left: 2px solid var(--text-color);
		border-right: 2px solid var(--text-color);
	}
</style>
