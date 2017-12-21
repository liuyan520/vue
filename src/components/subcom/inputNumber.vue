<template>
	<div>
		<b @click="subtraction">-</b>
		<input id="count" type="text" v-model="count">
		<b @click="add">+</b>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				count:1
			}
		},
		methods:{
			subtraction(){
				this.count--;
				if(this.count<1){
					this.count = 1;
				}
				this.sendcount();
			},
			add(){
				this.count++;	
				this.sendcount();
			},
			sendcount(){
				this.$emit("send",this.count);
			}
		}
	}
</script>

<style scoped>
	div{
		font-size: 12px;
		display: inline-block;
	}
	b{
		display: inline-block;
		width: 20px;
		height: 20px;
		text-align: center;
		border: 1px solid #BDC0C4;
	}
	input#count{
		width: 30px;
		height: 20px;
		padding: 0;
		margin: 0;
		color: #000;
		font-size: 14px;
		text-align: center;
	}
</style>