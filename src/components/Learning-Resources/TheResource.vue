<template >
<base-card>
<base-button @click="setSelectedTab('stored-resources')"
:mode="setStoreActiveTab"
>Stored Resources</base-button>
<base-button @click="setSelectedTab('add-resource')"
:mode="setAddActiveTab">Add Resources</base-button>
</base-card>
<keep-alive>
<component :is="selectTab"></component>
</keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResources.vue';
export default {
	components:{
		StoredResources,
		AddResource
	},
	computed:{
		setActiveTab(){
			return this.selectTab === 'stored-resources'? 'null': 'flat'
		},
		setAddActiveTab(){
			return this.selectTab === 'add-resource'? 'null': 'flat'
		}
	},
	data(){
		return{
			selectTab: 'stored-resource',
				storedResources:[
				{
					id: 'offical-guide',
					title: 'offical -guide',
					description: 'test document',
					link: 'https://vuejs.org'
			},
			{
					id: 'offical-google',
					title: 'offical -guide',
					description: 'test document',
					link: 'https://google.com'
			}
			]

		}
	},
	provide(){
		return{
			resources : this.storedResources,
			addResource: this.addResources,
			removeResource: this.removeResource
		}
	},
	methods:{
		setSelectedTab(tab){
			this.selectTab = tab;
		},
		addResources(title, description, url){
			const newResource ={
				id : new Date().toISOString(),
				title: title,
				description: description,
				link: url
			}
			this.storedResources.unshift(newResource);
			this.selectTab= 'stored-resources'; 
		},
		removeResource(resId){
			//this.storedResources = this.storedResources(res => res.id !== resId)
		const resIndex = this.storedResources.findIndex(res => res.id === resId);
		this.storedResources.splice(resIndex,1);
		},
	}
}
</script>

<style scoped>


</style>