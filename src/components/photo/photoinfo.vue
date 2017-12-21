<template>
	<div id="tmpl">
		<h3>{{list.title}}</h3>
		<span>{{list.add_time | datefmt("YYYY-MM-DD HH:mm:ss")}}</span>
		<span>点击次数{{list.click}}</span>
		<div class="mui-content">
		    <ul class="mui-table-view mui-grid-view mui-grid-9">
		        <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3" v-for="(item, index) in photos">
		            <img class="preview-img" :src="item.src" height="100" @click="$preview.open(index,photos)">
		        </li>
		     
		    </ul> 
		</div>
		<comment :zid="imgid"></comment>

	</div>
</template>

<script>
  	import common from "../../kits/common.js";
  	import comment from "../subcom/comment.vue"
	export default{
		components:{
			comment
		},
		data(){
			return{
				list:{},
				imgid:0,
				photos:[]
			}
		},
		created(){
			this.imgid = this.$route.params.imgid;
			this.getphotoinfo();
			this.getphotos();
		},
		methods:{
			getphotoinfo(){
				var url = common.apidomain + "/api/getimageInfo/" +this.imgid;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.list = data.message[0];
				})
			},
			getphotos(){
				var url = common.apidomain + "/api/getthumimages/" +this.imgid;
				this.$http.get(url).then(function(res){
					var data = res.body;
					if(data.status!=0){
						alert(data.message);
						return;
					}
					this.photos = data.message;
					for(var i=0;i<this.photos.length;i++){
						this.photos[i].w = 600;
						this.photos[i].h = 400;
					}
				})
			}
		}
	}

</script>

<style scoped>
	img{
		width: 150px;
		height: 150px;
	}
</style>