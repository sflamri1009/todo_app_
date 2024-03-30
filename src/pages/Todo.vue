<template>
  <q-page class="bg-grey-3 column">
	<div class="row q-pa-sm bg-primary">
      <q-input 
      class="col"
      @keyup.enter="addTask"
      filled 
      square
      v-model="newTask" 
      placeholder="tambah tugas" 
      dense
      bg-color="white">
        <template v-slot:append>
          <q-btn 
          @click="addTask"
          round 
          dense 
          flat 
          icon="add" />
        </template>
      </q-input>
	</div>
	  <div>
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
			@click.stop="deleteTask(index)"
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
	  <div 
	  v-if="!tasks.length"
	  class="no-tasks absolute-center">
		<q-icon
		name="check"
		size="100px"
		color="primary"/>
		<div class="text-h5 text-primary text-center"> 
		TAK ADA TUGAS
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
		  color: ref(['teal'])
		}
	  },
	data(){
		return{
			newTask:'',
			tasks:[
				//~ {
				//~ title:'get bananas',
				//~ done:false
				//~ },
				//~ {
				//~ title:'eat bananas',
				//~ done:true
				//~ },
				//~ {
				//~ title:'poo bananas',
				//~ done:false
				//~ },
			]
			}
		},
	
	methods:{
		deleteTask(index) {
		  this.$q.dialog({
			title: 'Confirm',
			message: 'Yakin mau hapus task?',
			cancel: true,
			persistent: true
		  }).onOk(() => {
			this.tasks.splice(index, 1)
			this.$q.notify('Task dihapus')
		  })				 
		},
		addTask() {
		//~ console.log('addTask')
		this.tasks.push({
			title: this.newTask,
			done: false
			})
			this.newTask = ''
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
	.no-tasks{
		opacity:0.5;
		}
</style>
