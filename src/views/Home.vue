<template>
  <div class="home">
		<FilterNav @filterChange="currentFilter = $event" :currentFilter="currentFilter"/>
		<div v-if="projects.length">
			<div v-for="project in projects" :key="project.id"> 
				<Project :project="project" @delete="handleDelete" @complete="handleComplete" 
					:class="{ hidden: (currentFilter ===  'completed' && project.complete === false)
						|| (currentFilter ===  'ongoing' && project.complete === true)
					}"
				/>
			</div>
		</div>
  </div>
</template>

<script>
import Project from '../components/Project.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
	data() {
		return {
			projects: [],
			currentFilter: 'all'
		}
	},
  components: {
		Project,
		FilterNav
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

<style>
  .filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #555;
  }
	.hidden {
		display: none
	}
</style>
