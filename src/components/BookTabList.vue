<template>
	<div class="tab_list">
		<div class="items" v-for="(item,index) in list" :key="index">
			<i v-if="item.tips" :style="item.tips==='热'?'border-left-color:#e76648':'border-left-color:#393'"></i>
			<span class="tips" v-if="item.tips">{{item.tips}}</span>
			<h3>{{item.title}}</h3>
			<p>{{item.des}}</p>
			<div class="imgs">
				<div v-for="(subitem,subindex) in item.imgs" :key="subindex"><img :src="subitem" alt=""></div>
				<div class="plus">+{{item.plus}}</div>
			</div>
		</div>
	</div>
</template>
<style lang="scss" scoped>
	.tab_list{
		width: 100%;
		background-color: #eee;
		overflow: hidden;
		.items{
			width: 94%;
			margin: 3%;
			padding: 20px;
			overflow: hidden;
			box-sizing:border-box;
			background-color: #fff;
			position: relative;
			h3{
				color: #494949;
				font-size: 19px;
				line-height: 1.4;
			}
			p{
				color: #9b9b9b;
				line-height: 1.4;
				font-size: 13px;
				margin: 10px 0;
			}
			i{
				font-size: 0;
				position: absolute;
				left: 0;
				top: -36px;
				border: 36px solid transparent;
				border-left-color: #393;
			}
			.tips{
				position: absolute;
				left: 0;
				top: 0;
				color: #fff;
				z-index: 100;
			}
			.imgs{
				display: flex;
				width: 100%;
				height: 70px;
				align-items:center;
				div{
					margin-right:5px;
				}
				.plus{
					margin-left: 10px;
					color: #e76648;
					font-size: 18px;
					opacity: .8;
				}
				img{
					width: 50px;
					height: 70px;
				}
			}
		}
	}
</style>
<script>
	export default{
		data(){
			return{
				list:[]
			}
		},
		created(){
			this.$http
            .get("/data/book_tab_list.json")
            // 监听返回
            .then(({ data }) => {
              this.list=data;
              console.log(this.list);
            })
		}
	}
</script>