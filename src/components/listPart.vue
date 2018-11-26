<template>
		<ul v-cloak>
			<router-link  v-for="(item, index) in data" :key="index" class="part" tag="li" to="/home">
				<img :src="'/pic/'+item.img" alt="">
				<h3>{{item.title}}</h3>
				<div class="rating">
					<div class="Stars">
					</div>
					<span>{{(Math.round((item.rating)*10)/10).toFixed(1)}}</span>
				</div>	
			</router-link>	
		</ul>
</template>

<style type="text/css" lang="scss" scoped>
@import '../base.scss';
[v-cloak] {
	display: none;
}
ul {
	height: 186px;
	white-space: nowrap;
    width: 100%;
	overflow-x:auto; 
	li {
		/* float: left; */
		display: inline-block;
		width: 100px;
		text-align: center;
		margin-right: 8px;
		img {
			display: block;
			width: 100px;
			height: 100px;
		}
		h3 {
			margin-top: 3px;
			font-size: 14px;
			font-weight: normal;
			white-space: nowrap;
			text-overflow: ellipsis;
			overflow: hidden;
		}
		.rating {
			font-size: 12px;
			color: #B3B3B3;
		}
	}
}
</style>

<script type="text/javascript">
	export default {
		props: ['data', 'classify'],
		created() {
		}	
	}
</script>