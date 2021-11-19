<template>
	<div>
		<h1>{{continent}}: {{ mountain }}</h1>
		<!-- <p v-if="$fetchState.pending">
			<span class="loading"></span>
		</p>
		<p v-else-if="$fetchState.error">Error while fetching mountains 🤬</p> -->
		<section class="content">
			<img :src="image" :alt="mountain"/>
			<p id="description">{{description}}</p>
		</section>
		<NuxtLink to="/getMountain">Back to Mountains</NuxtLink>
	</div>
</template>
<script>
export default {
	async asyncData({params,redirect}) {
		const mountains = await fetch(
			'https://api.nuxtjs.dev/mountains'
		).then((res) => res.json())	
		
		const filteredMountain = mountains.find(
			(el) => 
				el.continent.toLowerCase() === params.continent && el.slug === params.mountain
		)

		if(filteredMountain){
			return{
				continent:filteredMountain.continent,
				mountain:filteredMountain.title,
				description:filteredMountain.description,
				image:filteredMountain.image
			}
		}else{
			redirect('/getMountain')
		}
	}
}
</script>
<style>
.content{
	margin-bottom: 30px;
}
#description{
	margin-top: 30px;
}
</style>