<template>
	<div id="tmpl">
		<div class="title">
			图文列表
		</div>
		<ul class="mui-table-view">
			<li class="mui-table-view-cell mui-media" v-for="item in list">
				<router-link v-bind="{to:'/news/newsinfo/'+item.id}">
					<img class="mui-media-object mui-pull-left" :src="item.img_url">
					<div class="mui-media-body">
						{{item.title}}
						<p class='mui-ellipsis' v-text="item.zhaiyao"></p>
						<span>发表时间：{{item.add_time | datefmt('YYYY-MM-DD HH:mm:ss')}}</span>
						<span v-text="'点击数：'+item.click"></span>
					</div>
				</router-link>
			</li>
			
		</ul>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				list:[]
			}
		},
		created(){
			this.getnewslist();
		},
		methods:{
			getnewslist(){
				var url = "http://www.lovegf.cn:8899/api/getnewslist";
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status != 0){
						alert(data.message);
					}
					this.list = data.message;
				})
			}
		}
	}
</script>

<style scoped>
	.mui-table-view .mui-media-object {
		width: 50px;
		height: 50px;
		max-width: 50px;
	}
</style>