<!-- 以后项目的根组件 -->
<template>
	<div>
		<!-- 1.0 template主要是放html元素的（html的页面结构） -->
		<mt-header fixed title="刘艳vue网页初始"></mt-header>
		<router-view></router-view>
		<nav class="mui-bar mui-bar-tab">
			<router-link class="mui-tab-item " to="/home">
				<span class="mui-icon mui-icon-home"></span>
				<span class="mui-tab-label">首页</span>
			</router-link>
			<router-link class="mui-tab-item" to="/tabbar-with-chat">
				<span class="mui-icon mui-icon-email"></span>
				<span class="mui-tab-label">会员</span>
			</router-link>
			<router-link class="mui-tab-item" to="/shopcar">
				<span class="mui-icon mui-icon-contact">
					<span class="mui-badge">0</span>
				</span>
				<span class="mui-tab-label">购物车</span>
			</router-link>
			<router-link class="mui-tab-item" to="/tabbar-with-map">
				<span class="mui-icon mui-icon-gear"></span>
				<span class="mui-tab-label">搜索</span>
			</router-link>
		</nav>
	
	</div>
</template>

<script>
	import {vm,COUNTSTR} from "./kits/vm.js";
	vm.$on(COUNTSTR,function(input){
		var badge = document.querySelector('.mui-badge');
		badge.innerText = parseInt(badge.innerText) + input.count;
	})
	export default{
		data(){
			return{

			}
		},
		created(){

		},
		methods:{

		}
	}
</script>

<style scoped>
	
	
</style>
