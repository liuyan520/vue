<template>
	<div id="tmpl">
		<div class="title">{{list.title}}</div>
		<div class="content" v-html="list.content"></div>
	</div>
</template>

<script>
	import common from "../../kits/common.js"
	export default{
		data(){
			return{
				id:0,
				list:[]
			}
		},
		created(){
			this.id = this.$route.params.id;
			this.getgoodsdesc();
		},
		methods:{
			getgoodsdesc(){
				var url = common.apidomain + "/api/goods/getdesc/" +this.id;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = data.message[0];
				})
			}
		}
	}
</script>

<style scoped>
	#tmpl{
		padding: 0 10px;
	}
	.title{
		color: blue;
		line-height: 50px;
		border-bottom: 1px solid #BDC0C4;
	}
	.content{
		font-size: 14px;
	}
</style>