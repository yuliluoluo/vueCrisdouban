<template>
	<div class="outer">
		<mt-swipe :auto="4000" class="swipe">
			<mt-swipe-item class="items" v-for="(item,index) in imgs" :key="index" :style="'background-image:url('+item+')'">
			</mt-swipe-item>
		</mt-swipe>
		<div class="tabs">
			<div class="left">
				<div class="tab" v-for="(item,index) in tabs" :key="index" @click="changeTab(item,index)" :style="item.isActive?'border-bottom-color:#f00;color:#333;':'color: #9b9b9b;border-bottom-color:transparent'">{{item.text}}</div>
			</div>
			<div class="iconfont icon-gouwuche"></div>
		</div>
		<component :is="tab_content" class="tabs_content"></component>
	</div>
</template>
<style lang="scss" scoped>
	.outer{
		width: 100%;
		height: 100%;
		font-family: PingFang SC,Helvetica Neue,Helvetica,Roboto,Arial,Noto Sans CJK SC,Source Han Sans CN,Lantinghei SC,Microsoft Yahei,Hiragino Sans GB,WenQuanYi Micro Hei,sans-serif;
		.swipe{
			width: 100%;
			height: 150px;
			.items{
				width: 100%;
				height: 150px;
				background-size: contain;
			}
		}
		.tabs{
			width: 100%;
			overflow: hidden;
			text-align: center;
			.left{
				height: 100%;
				display: flex;
				float: left;
				width: 80%;
				align-items:center;
				color: #9b9b9b;
				.tab{
					flex:1;
					padding: 10px;
					border-bottom: 2px solid transparent;
				}
			}
			.icon-gouwuche{
				float: right;
				width: 19%;
				height: 100%;
				padding-top: 10px;
				font-size: 25px;
			}
		}
	}
	.tabs_content{
		width: 100%;
	}
</style>
<script>
import BookBuy from './BookBuy.vue';
import BookActivity from './BookActivity.vue';
import BookTabList from './BookTabList.vue';
	export default {
		components:{
			BookBuy,
			BookActivity,
			BookTabList
		},
		data(){
			return {
				imgs:["https://img1.doubanio.com/view/freyr_page_photo/raw/public/3128.jpg",
				"https://img1.doubanio.com/view/freyr_page_photo/raw/public/3069.jpg",
				"https://img3.doubanio.com/view/freyr_page_photo/raw/public/3171.jpg",
				"https://img3.doubanio.com/view/freyr_page_photo/raw/public/3180.jpg"],
				tabs:[{isActive:false,text:"活动"},
						{isActive:true,text:"新书"},
						{isActive:false,text:"书单"}],
				tab_content:"BookBuy",
				tab_content_arr:["BookActivity","BookBuy","BookTabList"]
			}
		},
		methods:{
			changeTab(item,index){
				this.tabs.forEach(i=>{
					i.isActive=false;
				});
				item.isActive=true;
				this.tab_content=this.tab_content_arr[index];
			}
		}
	}
</script>