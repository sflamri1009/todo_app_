<template>
  <q-page class="bg-grey-3 column">
	  <div>
		<div class="q-pa-md q-gutter-sm">
		    <q-btn label="Confirm" color="primary" @click="confirm = true" />
			<q-dialog v-model="confirm" persistent>
			  <q-card>
				<q-card-section class="row items-center">
				  <q-avatar icon="signal_wifi_off" color="primary" text-color="white" />
				  <span class="q-ml-sm">Anda akan menghapus todo ini</span>
				</q-card-section>

				<q-card-actions align="right">
				  <q-btn flat label="Cancel" color="primary" v-close-popup />
				  <q-btn flat label="OK" color="primary" @click.stop="deleteTask(index)" v-close-popup />
				</q-card-actions>
			  </q-card>
			</q-dialog>		    		
		</div>
		
		
		<div class="q-gutter-sm">
		<q-list 
		separator
		bordered
		class="bg-white">
		  <q-item 
		  v-for="(task, index) in tasks"
		  :key="task.title"
		  @click="task.done = !task.done" 
		  :class= "{'done bg-blue-1' : task.done}"
		  clickable
		  v-ripple>
			<q-item-section avatar>
			  <q-checkbox 
			  v-model="task.done"
			  color="primary" 
			  class="no-pointer-events"/>
			</q-item-section>
			<q-item-section>
			  <q-item-label>{{ task.title }}</q-item-label>
			</q-item-section>
			<q-item-section
			v-if="task.done"
			side
			>					
			<q-btn
			@click="confirm = true"
			flat
			round
			dense
			color="primary"
			icon="delete"
			></q-btn>
			</q-item-section>
		  </q-item>

		</q-list>
		</div>
	  </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import { ref } from 'vue'

export default defineComponent({
	  setup () {
		return {
		  color: ref(['teal']),
		  confirm: ref(false)
		}
	  },
	data(){
		return{
			tasks:[
				{
				title:'get bananas',
				done:false
				},
				{
				title:'eat bananas',
				done:true
				},
				{
				title:'poo bananas',
				done:false
				},
			]
			}
		},
	
	methods:{
		deleteTask(index) {
			this.tasks.splice(index, 1)
			}
		
		}
	
})
</script>

<style lang="scss">
	.done{
		.q-item__label{
			text-decoration:line-through;
			color:#bbb
			}
		}
	
</style>
