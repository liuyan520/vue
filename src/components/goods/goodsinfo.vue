<template>
	<div id="tmpl">
		<div class="slider">
			<slider :imgs="list"></slider>
		</div>

		<div class="goodsinfo">
			<div class="title">{{info.title}}</div>
			<div class="price">
				<span>市场价：￥<del>{{info.market_price}}</del></span>
				<span>销售价：￥<b style="color:red; font-size:16px;">{{info.sell_price}}</b></span>
			</div>
			<div class="acount">
				购买数量：<inputNumber @send="getcount"></inputNumber>
			</div>
			<div class="btn">
				<mt-button size="small" type="primary">立即购买</mt-button>
				<mt-button size="small" type="danger" @click="toshopcar">加入购物车</mt-button>
			</div>
			<div class="goodsparam">
				<div class="words">商品参数</div>
				<div class="subwords">
					<ul>
						<li>商品货号:{{info.goods_no}}</li>
						<li>商品库存:{{info.stock_quantity}}件</li>
						<li>上架时间:{{info.add_time | datefmt("YYYY-MM-DD HH:mm:ss")}}</li>
					</ul>
				</div>
			</div>
		</div>
		<router-link style="color:#fff;" v-bind="{to:'/goods/goodsdesc/'+info.id}"><mt-button type="primary" size="large">图文详情</mt-button></router-link>
		<router-link style="color:#fff;" v-bind="{to:'/goods/goodscomment/'+info.id}"><mt-button type="danger" size="large">商品评论</mt-button></router-link>
	</div>
</template>

<script>
	import common from "../../kits/common.js";
	import slider from "../subcom/slider.vue";
	import inputNumber from "../subcom/inputNumber.vue";
	import {vm,COUNTSTR} from "../../kits/vm.js";
	
	export default{
		components:{
			slider,
			inputNumber
		},
		data(){
			return{
				list:[],
				goodsid:0,
				info:[],
				count:1
			}
		},
		created(){
			this.goodsid = this.$route.params.goodsid;
			this.getgoodsimg();
			this.getgoodsinfo();
		},
		methods:{
			getgoodsimg(){
				var url = common.apidomain + "/api/getthumimages/" +this.goodsid;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = data.message;
					for(var i=0;i<this.list.length;i++){
						this.list[i].src="http://vue.studyit.io/"+this.list[i].src;
					}
				})
			},
			getgoodsinfo(){
				var url = common.apidomain + "/api/goods/getinfo/" +this.goodsid;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.info = data.message[0];
				})
			},
			getcount(input){
				this.count = input;
			},
			toshopcar(){
				vm.$emit(COUNTSTR,{'count':this.count,'goodsid':this.goodsid})
			}
		}
	}
</script>

<style scoped>	
	#tmpl{
		padding: 0 5px;
	}
	.slider{
		border: 1px solid #BDC0C4;
	}
	.goodsinfo .title{
		font-size: 16px;
		color: blue;
		margin: 10px 0;
		line-height: 50px;
		border: 1px solid #BDC0C4;
	}
	.goodsinfo .price{
		font-size: 12px;
	}
	.goodsinfo .acount{
		margin: 5px 0;
	}
	.goodsinfo .goodsparam{
		margin: 10px 0;
		border: 1px solid #BDC0C4;
	}
	.goodsinfo .goodsparam .words{
		padding-left: 30px;
		line-height: 40px;
		border-bottom: 1px solid #BDC0C4;
	}
	.goodsinfo .goodsparam .subwords li{
		font-size: 14px;
		list-style: none;
	}
</style>