<template>
	<nav class="filter-nav">
		<button @click="updateFilter('all')"
			:class="{ active: currentFilter === 'all'}"
		>
			View All
		</button>
		<button @click="updateFilter('completed')"
			:class="{ active: currentFilter === 'completed'}"
		>
			View Completed
		</button>
		<button @click="updateFilter('ongoing')"
			:class="{ active: currentFilter === 'ongoing'}"
		>
			View Ongoing
		</button>
	</nav>
</template>

<script>
export default {
	props: ['currentFilter'],
	methods: {
		updateFilter(filter) {
			this.$emit('filterChange', filter)
		}
	}
}
</script>

<style>

</style>
