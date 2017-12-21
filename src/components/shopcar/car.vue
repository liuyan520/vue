<template>
	<div id="tmpl">
		<ul>
			<li v-for="item in list">
				<div class="btn">
					<button>按钮</button>
				</div>
				<div class="img">
					<img :src="item.thumb_path" alt="">
				</div>
				<div class="title">{{item.title}}</div>
				<div class="price">￥{{item.sell_price}}</div>
				<inputNumber></inputNumber>
				<div class="del">
					<a href="">删除</a>
				</div>
			</li>
		</ul>
	</div>
</template>

<script>
	import common from "../../kits/common.js";
	import inputNumber from "../subcom/inputNumber.vue"
	export default{
		components:{
			inputNumber
		},
		data(){
			return{
				list:[],
				id:87
			}
		},
		created(){
			this.getcarlist();
		},
		methods:{
			getcarlist(){
				var url =common.apidomain + "/api/goods/getshopcarlist/" + this.id;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = data.message;
					for(var i=0;i<this.list.length;i++){
						this.list[i].thumb_path = "http://vue.studyit.io/"+this.list[i].thumb_path;
					}
				})
			}
		}
	}
</script>

<style scoped>
	ul,li,div{
		margin: 0;
		padding: 0;
	}
	#tmpl{
		padding: 0 10px;
	}
	li{
		list-style: none;
		margin: 10px 0;
		position: relative;
		border-bottom: 1px solid #BDC0C4;
		height: 100px;
	}
	li>div{
		position: absolute;
	}
	img{
		width: 60px;
		height: 60px;
	}
	.btn{
		top: 30px;
		left: 0;
	}
	.img{
		top: 20px;
		left: 65px;
	}
	.title{
		top: 5px;
		left: 140px;
		color: #26A2FF;
		font-weight: bold;
		font-size: 16px;
	}
	.price{
		top: 60px;
		left: 140px;
		color: red;
	}
	div[data-v-8a38ad04]{
		top: 60px;
		left: 210px;
	}
	.del{
		top: 60px;
		left: 350px;
		font-size: 14px;
		color: #26A2FF;
	}

</style>