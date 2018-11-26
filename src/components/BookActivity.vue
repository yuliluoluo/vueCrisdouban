<template>
	<div class="list">
		<div class="items" v-for="(item,index) in list" :key="index">
			<div class="top" :style="'background-image:url('+item.url+')'">
				<div class="mask">
					<div class="titles">
						<h2>{{item.title}}</h2>
						<p>{{item.subTitle}}</p>
					</div>
				</div>
			</div>
			<div class="bottom">
				<p class="des">
					{{item.des}}
				</p>
				<p class="icons"><span class="iconfont icon-ren"></span><span>{{item.people}}人参与</span><span :style="item.tips==='未开始'?'background-color:#193':'background-color:#ccc'">{{item.tips}}</span></p>
			</div>
		</div>
	</div>
</template>
<style lang="scss" scoped>
	.list{
		width: 100%;
		overflow:hidden;
		background-color: #eee;
		.items{
			width: 94%;
			height: 220px;
			margin: 5% 3%;
			background-color: #fff;
			.top{
				height: 120px;
				text-align: center;
				color: #fff;
				background-size: contain;
				.mask{
					display: flex;
					align-items:center;
					width: 100%;
					height: 100%;
					opacity: .7;
					background-color: #666;
				}
				.titles{
					width: 100%;
					text-align: center;
				}
				h2{
					font-size: 21px;
					font-weight: 500;
					margin-bottom: 5px;
				}
				p{
					font-size: 14px;
				}
			}
			.bottom{
				width: 100%;
				height: 80px;
				padding: 10px;
				.des{
					font-size: 14px;
					color: #666;
					padding: 20px 0;
				}
				.icons{
					font-size: 14px;
					color: #333;
					span:last-child{
						margin-left: 10px;
						color: #fff;
						padding: 2px 10px;
						font-size: 12px;
						background-color: #ccc;
					}
					.icon-ren{
						font-size: 20px;
						margin-right: 10px;
						color: #dd3388;
					}
				}
			}
		}
	}
</style>
<script>
	export default {
		data(){
			return {
				list:[]
			}
		},
		created(){
			this.$http
            .get("/data/book_activity.json")
            // 监听返回
            .then(({ data }) => {
              this.list=data;
              console.log(this.list);
            })
		}
	}
</script>