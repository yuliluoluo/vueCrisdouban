<template>
<div>
	<div class="commentTitle">精彩短评</div>
	<mt-loadmore  :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore"  bottomPullText="">
		<div class="commentItem" v-for="(item, index) in data.interests" :key="index">
			<div class="user">
				<div class="pic">
					<img :src="item.user.avatar">
				</div>
				<div class="info">
					<div class="top">
						<div class="username">{{item.user.name}}</div>
						<el-rate :disabled="true" class="start" v-model="item.start"></el-rate>
					</div>
					<div class="time">{{item.create_time}}</div>
				</div>
			</div>
			<div class="content">{{item.comment}}</div>
		</div>
	</mt-loadmore>
	<!-- <div class="loadComment" @click="loadComment">
		<div>查看更多评论</div>
		<div>三</div>
	</div> -->
</div>
</template>
<style type="text/css" lang="scss" scoped>
.commentTitle {
	border-top: 1px solid #efefef;
	border-bottom: 1px solid #efefef;
	box-shadow: 0 -1px 5px #efefef;
	background-color: #fafafa;
	margin-top: 10px;
	height: 50px;
	font-size: 20px;
	padding-left: 20px;
	line-height: 50px;
}
.commentItem {
margin: 10px 0;
.user {
	height: 50px;
	padding: 10px 10px;
	font-size: 16px;
	.pic {
		width: 50px;
		height: 50px;
		border-radius: 50%;
		overflow: hidden;
		float: left;
		margin-right: 10px;
		img {
			width: 100%;
		}
	}
	.info {
		.top {
			line-height: 30px;
			height: 30px;
			display: flex;
			.username {
				margin-right: 5px;
			}
			.start {
				margin-top: 5px;
			}
		}
		.time {
			font-size: 12px;
			color: #666;
			line-height: 20px;
		}
	}
}
.content {
	font-size: 14px;
	padding: 0 10px 0 70px;;
	line-height: 1.5;
	color: #666;
}
}
/* .loadComment {
	height: 50px;
	background-color: #f0f0f0;
	text-align: center;
	line-height: 30px;
	font-size: 16px;
	margin: 0px;
	margin-top: 20px;
	overflow: hidden;
	border-top: 1px solid #ccc;
	box-shadow: 0 -1px 5px #ccc;
} */
</style>
<script type="text/javascript">
import { Toast } from 'mint-ui';
	export default {
		data() {
			return {
				num: 10,
				data: {},
				start: 5,
				allLoaded:false
			}
		},
		created(){
			this.$http
				.get('/data/comment.json')
				.then(({data}) => {
					console.log(data)
					data.interests.length = 10;
					data.interests.forEach(function(val) {
							val.start = 2 + Math.random() * 3;
					});
					return this.data = data;
				})
			},
		methods: {
			/*allLoaded(){
				
			},*/
			/*loadComment() {
			this.$http
				.get('/data/comment.json')
				.then(({data}) => {
					this.num += 10;
					data.interests.length = this.num;
					data.interests.forEach(function(val) {
							val.start = 2 + Math.random() * 3;
					});
					return this.data = data;
				})
			},*/
			loadBottom() {
				this.$http
				.get('/data/comment.json')
				.then(({data}) => {
					console.log(data.interests.length);
					if(this.num>=data.interests.length){
						console.log(this.num+"lalala");
						Toast({
						message: '数据加载完成',
						position: 'middle',
						duration: 5000
						});
						this.allLoaded = true;// if all data are loaded
						return;
					}
					this.num += 10;
					data.interests.length = this.num;
					data.interests.forEach(function(val) {
						val.start = 2 + Math.random() * 3;
					});
					return this.data = data;
				})
					this.$refs.loadmore.onBottomLoaded();
}
		}
	}
</script>