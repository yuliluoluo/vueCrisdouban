<template>
	<div id="like" @click="change" :class="like?'active':''">
		<span class="img"></span><span>{{newCount}}</span>
	</div>
</template>
<style>
	#like{
		width: 100px;
		height: 30px;
		line-height: 30px;
		display: flex;
		align-items:center;
		justify-content:center;
		font-size: 15px;
		margin: 30px auto;
		color: #42bd56;
		border: 1px solid #42bd56;
	}
	#like .img{
		margin-right: 4px;
		width: 20px;
		height: 20px;
		background:url(https://img3.doubanio.com/f/talion/c689ab2369da387f2cb0d4da4a22614d7f048bf9/pics/card/ic_heart_green.svg) no-repeat;
	}
	#like.active{
		color: #333;
		border: 1px solid #bfbfbf;
	}
	#like.active .img{
		background-image: url(https://img3.doubanio.com/f/talion/0129352875382ff0544020161709c2ae9b00c737/pics/card/ic_heart_red.svg);
	}
</style>
<script>
	export default{
			props:{
				count:{
					type: Number,
					required: false,
				},
				localid:{
					type:String,
					required:true
				}
			},
			data:function () {
				return {
					like:localStorage.getItem(this.localid),
					newCount:this.count
				}
			},
				methods:{
				change:function () {
					this.like=!this.like;
					localStorage.setItem(this.localid,this.like);
					console.log(this.like,111);
					if(this.newCount!=undefined){
						if(this.like){
							this.newCount++;
						}else{
							this.newCount--;
						}
					}
				}
			}
	}
</script>