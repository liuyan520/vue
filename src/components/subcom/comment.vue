<template>
	<div>
		<h4>提交评论</h4>
		<textarea placeholder="请输入评论内容" v-model="info"></textarea>
		 <button type="button" class="mui-btn mui-btn-primary mui-btn-block" @click="postcomment">发表</button>
		 <h4>评论列表</h4>
		 <div style="border-bottom:1px solid #000" v-for="item in list">
		 	<div>{{item.content}}</div>
		 	<span style="font-size:10px">{{item.user_name}}</span>
		 	<span style="font-size:10px">发表时间：{{item.add_time | datefmt('YYYY-MM-DD HH:mm:ss')}}</span>
		 </div>
		 <button type="button" class="mui-btn mui-btn-primary mui-btn-block" @click="getmore">加载更多</button>
	</div>
</template>

<script>
	import common from "../../kits/common.js";
	import {Toast} from "mint-ui";
	export default{
		data(){
			return{
				id:10,
				list:[],
				info:'',
				pageindex:1
			}
		},
		props:['zid'],
		created(){
			// this.id = this.$route.params.id;
			this.getcomment(this.pageindex);
			// this.postcomment();  /*点击事件触发不用在这写*/
		},
		methods:{
			getcomment(pageindex){
				pageindex = pageindex || 1;
				var url = common.apidomain+'/api/getcomments/'+this.zid+'?pageindex='+pageindex;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = this.list.concat(data.message);
				})
			},
			postcomment(){
				var url = common.apidomain+'/api/postcomment/'+this.zid;
				this.$http.post(url,{content:this.info},{emulateJSON:true}).then(function(res){
						var data = res.body;
						Toast(data.message);
						this.list = [{"user_name": "匿名用户",
						 "add_time": new Date(),
						 "content": this.info}].concat(this.list);
						this.info='';
						this.getcomment(this.pageindex);
				})
			},
			getmore(){
				this.pageindex++;
				this.getcomment(this.pageindex);
			}  
		}
	}
</script> 

<style scoped>
	
</style>