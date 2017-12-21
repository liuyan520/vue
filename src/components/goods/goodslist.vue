<template>
	<div id="tmpl">
		<div class="mui-content" style="background-color:#fff">
		   <ul class="mui-table-view mui-grid-view">
		       <li class="mui-table-view-cell mui-media mui-col-xs-6" v-for="item in list">
		           <router-link v-bind="{to:'/goods/goodsinfo/'+item.id}">
		               <img class="mui-media-object" :src="item.img_url">
		               <div class="mui-media-body" v-text="item.zhaiyao"></div>
		               <div class="masker">
		               		<span style="color:red;">{{item.sell_price}}</span>&nbsp&nbsp&nbsp<span><del>{{item.market_price}}</del></span>
		               </div>

		           </router-link>
		       </li>
		   </ul>  
		    <button type="button" class="mui-btn mui-btn-primary mui-btn-block" @click="getmore()">加载更多</button> 
		</div>
	</div>
</template>

<script>
	import common from "../../kits/common.js";
	import { Toast } from 'mint-ui'; 
	export default{
		data(){
			return{
				list:[],
				pageindex:1
			}
		},
		created(){
			this.getgoodslist();
		},
		methods:{
			getgoodslist(){
				var url = common.apidomain+"/api/getgoods?pageindex="+this.pageindex;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status != 0 ){
						Toast(res.body.message);
						return;
					}

					this.list = this.list.concat(data.message);
				})
			},
			getmore(){
				this.pageindex++;
				this.getgoodslist();
			}
		}
	}
</script>

<style scoped>
    .mui-table-view-cell{
    	border: 1px solid #000;
    }
	.mui-media-body{
		height: auto !important;
		font-size: 14px !important;
		text-align: left;
	}
	.mui-table-view-cell > a:not(.mui-btn) {
		white-space: normal !important;
	}
	.masker{
		height: 50px;
		background-color: rgba(0, 0, 0, 0.1);
	}
</style>