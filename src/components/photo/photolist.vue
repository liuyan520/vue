<template>
	<div id="tmpl">
		<div id="tab">
			<ul id="nav" :style="'width:'+ ulwidth +'px;'">
			    <li @click="getphotolist(0)">全部</li>
				<li v-for="item in nav" v-text="item.title" @click="getphotolist(item.id)"></li>
			</ul>
		</div>
		<div id='list'>
			<ul>
				<li v-for="item in list">
					<router-link v-bind="{to:'/photo/photoinfo/'+item.id}" style="width:100%;height:300px;display:block;">
						<!-- <div class="img"></div> -->
						<img v-bind="{src:'http://vue.studyit.io/'+item.img_url}" alt="">
						<div class="masker">
							<div v-text="item.title"></div>
							<div v-text="item.zhaiyao"></div>
						</div>
					</router-link>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	import common from "../../kits/common.js";
	// import { Lazyload } from 'mint-ui';
	export default{
		data(){
			return{
				nav:[],
				ulwidth: 0,
				list:[]
			}
		},
		created(){
			this.getphotoclassify();
			var all = 0;
			this.getphotolist(all);
		},
		methods:{
			getphotoclassify(){
				var url = common.apidomain+'/api/getimgcategory';
				var nav = document.getElementById('nav');
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.nav = data.message;
					this.ulwidth = 72*(data.message.length+1);
				});
			},
			getphotolist(cateid){
				cateid = cateid || 0;
				var url = common.apidomain+'/api/getimages/'+cateid;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = data.message;
				})
			}
		}
	}
</script>

<style scoped>
	*{
		margin: 0;
		padding: 0;
	}
	#tab{
		width: 500px;
		height: 50px;
		overflow-x: auto;
	}
	#nav li{
		list-style: none;
		float: left;
		padding: 0 8px;
		line-height: 25px;
		font-size: 14px;
		white-space: nowrap;
		cursor: pointer;
	}
	#nav li:hover{
		color: blue;
	}
	
	#list li{
		list-style: none;
		position: relative;
		margin-top: 10px;
	}
	#list li img{
		width: 100%;
		height: 300px;
		border: 1px solid #000;
	}
	#list li .img{
		width: 100%;
		height: 300px;
		border: 1px solid #000;
	}
	#list li .masker{
		width: 100%;
		background-color: rgba( 0, 0, 0, 0.3);
		position: absolute;
		bottom: 0;
		font-size: 14px;
	}
</style>