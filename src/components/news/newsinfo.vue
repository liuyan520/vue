<template>
	<div id="tmpl">
		<h3>{{list.title}}</h3>
		<div>{{list.add_time}}点击次数{{list.click}}</div>
		<div v-html="list.content"></div>
		<comment :zid="id"></comment>
	</div>
</template>

<script>
	import common from '../../kits/common.js';
	import comment from '../subcom/comment.vue';
	export default{
		components:{
			comment
		},
		data(){
			return{
				id:0,
				list:{}
			}
		},
		created(){
			this.id = this.$route.params.id;
			this.getnewsinfo();
		},
		methods:{
			getnewsinfo(){
				var url = common.apidomain + '/api/getnew/'+this.id;
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
	
</style>