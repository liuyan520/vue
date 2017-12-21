<template>
	<!-- <div id="tmpl"> -->
		<mt-swipe :auto="2000">
		  <mt-swipe-item  v-for="item in imgs">
		  	<img :src="item.src" alt="">
		  </mt-swipe-item>
		</mt-swipe>
	<!-- </div> -->
</template>

<script>
	export default{
		props:['imgs']
	}
</script>

<style scoped>
	.mint-swipe{
		height: 300px;
	}
	.mint-swipe-item{
		text-align: center;
	}
</style>