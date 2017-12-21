<template>
	<div id="tmpl">
		<mt-swipe :auto="4000">
		  <mt-swipe-item v-for="item in list">
		  	<img :src="item.img">
		  </mt-swipe-item>
		</mt-swipe>
		<div class="mui-content">
		    <ul class="mui-table-view mui-grid-view mui-grid-9">
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/news/newslist">
		              <span><img src="../../statics/imgs/1.png"></span>
		              <div class="mui-media-body">新闻资讯</div></router-link></li>
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/photo/photolist">
		              <span><img src="../../statics/imgs/2.png"></span>
		              <div class="mui-media-body">图片分享</div></router-link></li>
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/goods/goodslist">
		              <span><img src="../../statics/imgs/3.png"></span>
		              <div class="mui-media-body">商品购买</div></router-link></li>
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/feedback">
		              <span><img src="../../statics/imgs/4.png"></span>
		              <div class="mui-media-body">留言反馈</div></router-link></li>
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/vide">
		              <span><img src="../../statics/imgs/5.png"></span>
		              <div class="mui-media-body">视频专区</div></router-link></li>
		      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/callme">
		              <span><img src="../../statics/imgs/6.png"></span>
		              <div class="mui-media-body">练习我们</div></router-link></li>
		    </ul> 
		</div>
	</div>
</template>

<script>
	import common from "../kits/common.js"
    import { Toast } from 'mint-ui';
    
	export default{
		data(){
			return{
				list:[]
			}
		},
		created(){
			this.getImg();
		},
		methods:{
			getImg(){
				var url = common.apidomain+'/api/getlunbo';
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status != 0){
						Toast(data.message);
						return;
					}
					this.list = data.message;
				})
			}
		}

	}
</script>

<style scoped>
	.mint-swipe{
		height: 300px;
	}
	.mint-swipe img{
		width: 100%;
		height: 100%;
	}
	.mui-content img{
		width: 40px;
		height: 40px;
	}
	.mui-grid-view.mui-grid-9 {
		background-color: #fff;
	}
	.mui-grid-view.mui-grid-9 .mui-table-view-cell{
		border-bottom: none;
		border-right: none;
	}
</style>

