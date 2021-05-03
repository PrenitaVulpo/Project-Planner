<template>
  <div class="home">
		<div v-if="projects.length">
			<div v-for="project in projects" :key="project.id"> 
				<Project :project="project" @delete="handleDelete" @complete="handleComplete"/>
			</div>
		</div>
  </div>
</template>

<script>
import Project from '../components/Project.vue'

export default {
  name: 'Home',
	data() {
		return {
			projects: []
		}
	},
  components: {
		Project,
	},
	mounted() {
		fetch('http://localhost:3000/projects')
			.then(response => response.json())
			.then(data => this.projects = data)
			.catch(error => console.log(error.message))
	},
	methods: {
		handleDelete(id) {
			this.projects = this.projects.filter(project => {
				return project.id !== id
			})
		},
		handleComplete(id) {
			let completedProject = this.projects.find(project => {
				return project.id === id
			})
			completedProject.complete = !completedProject.complete 
		}
	}
}
</script>
