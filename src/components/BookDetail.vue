<template>
<div>
<div class="inner">
	<h1>{{data.title}}</h1>
	<img :src="data.url">
	<p>{{data.card_subtitle}}</p>
	<p class="author">作者：{{data.author}}</p>
	<div class="clearfix"></div>
	<p id="showAll" :class="{ellpes:!showAll}">{{data.showAll}}}</p>
	<a @click="fun_showAll" href="javascript:void(0)">( {{showAll?"收起":"展开"}} )</a>
</div>
<Comment></Comment>
</div>
</template>
<!-- 样式 -->
<style type="text/css" lang="scss" scoped>
.inner {
	padding: 0 20px;
	h1 {
		font-weight: 500;
		padding: 20px 0;
	}
	img {
		float: right;
		width: 30%;
		margin-left: 10px;
	}
	&::after{
		content:"";
		display: block;
		clear: both;
	}
	.author{
		margin: 20px 0;
		font-size: 20px;
	}
	#showAll{
		color: #494949;
		font-size:15px;
	}
	.ellpes{
		text-overflow:ellipsis;
		overflow:hidden; 
		display:-webkit-box; 
		-webkit-line-clamp:3; /*这个数字是设置要显示省略号的行数*/ 
		-webkit-box-orient:vertical; 
	}
	a{
		text-decoration: none;
		color: #2f2;
	}
}
</style>
<script type="text/javascript">
import Comment from './Comment.vue';
export default {
    components: { Comment },
	data() {
		return {
			data: [],
			showAll:false,
		}
	},
	watch: {
		$route() {
			// 更新数据
			this.dataUpdate();
		}
	},
	methods: {
		fun_showAll(){
			this.showAll=!this.showAll;
		},
		// 更新数据的方法
		dataUpdate() {
			this.$http
				// get请求
				.get('/data/book_detail.json', {
					// query数据
					params: {
						id: this.$route.params.id
					}
				})
				// 监听数据返回
				.then(({ data }) => {
					/*let arr = [];*/
					let id = this.$route.params.id;
					/*for(var i in data) {
						arr = arr.concat(data[i])
					}*/
					let result = data.find(function(val) {
						return val.id == id;
					})
					this.data = result;
				})
		}
	},
	// 组件创建完成时候请求数据
	created() {
		// 更新数据
		this.dataUpdate();
	}
}
</script>