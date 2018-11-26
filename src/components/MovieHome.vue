<template>
<div class="movie">
	<div class="content">
		<div class="maintype" v-for="(item, index) in data" :key="index">
			<div class="head">
				<h3>{{item.subject_collection.name}}</h3>
				<router-link tag="div" :to="'/MovieBroews/classicB'+item.subject_collection.name.substring(0,4)" class="more">更多</router-link>
			</div>
			<MovieList :data="item.subject_collection_items"></MovieList>
		</div>
	</div>
	<div class="bottom-list">
            <ul>
                <router-link tag="li" :to="'/MovieBroews/'+item.id+'B'+item.title" v-for="(item, index) in browse" :key="index">
                    <span>{{item.title}}</span>
                    <span class="arrow">
                        <span class="arrow white"></span>
                    </span>
                </router-link>
            </ul>
    </div>
</div>
</template>
<style lang="scss" scoped>
@import '../base.scss';
.movie{
	width: 100%;
    background-color: #fff;
}
.content {
	padding-top: 20px;
}
.maintype {
	height: 270px;
	overflow: hidden;
}
.head {
	display: flex;
	height: 40px;
	line-height: 40px;
	h3 {
		flex: 9;
		font-size: 1.06rem;
		font-weight: 500;
		padding-left: 10px;
	}
	.more {
		flex: 1;
		color: green;
		font-size: 14px;
		margin-right: 20px;
	}
}
.bottom-list{
    width: 100%;
    ul{
        width: 100%;
        box-sizing:border-box;
        padding: 0 10px;
        display: flex;
        flex-wrap:wrap;
        li{
            display: flex;
            align-items:center;
            justify-content:space-between;
            flex: 0 0 50%;
            line-height: 2.64rem;
            border-top: 1px solid #eee;
            color: #42bd56;
            &:last-child{
                border-bottom: 1px solid #eee;
            }
            .arrow{
                @include arrow(10px ,#ccc,left);
                position: relative;
                left: -10px;
                top: 0;
                .white{
                    position: absolute;
                    left: -13px;
                    top: -10px;
                    border-left-color: #fff;
                }
            }
        }
    }
}
/* .container p {
	font-size: 24px;
	height: 50px;
	line-height: 50px;
	padding-left: 10px;
}
ul.type-list {
	padding: 0px 10px;
	li {
		width: 50%;
		float: left;
		box-sizing: border-box;
		border-bottom: 1px solid #ccc;
		border-right: 1px solid #ccc;
		height: 50px;
		line-height: 50px;
		font-size: 18px;
		padding-left: 10px;
		position: relative;
		&:first-child, &:nth-child(2) {
			border-top: 1px solid #ccc;
		}
		&:nth-child(2n) {
			border-right: none;
		}
		a {
			text-decoration: none;
			display: block;
			color: #42bd56;
		}
		.arrow {
			@include arrow(10px, #ccc, left);
			position: absolute;
			top: 15px;
			right: 4px;
			.white {
				position: absolute;
				top: -10px;
				right: -7px;
				border-left-color: #fff;
			}
		}
	}
} */
</style>
<script>
//引入组件
import MovieList from './MovieList.vue';
export default {
	data () {
		return {
			data : '',
			search : '',
			useData:'',
			browse : [
				{title: "经典", id: "classic"},
				{title: "冷门佳片", id: "underrated"},
				{title: "豆瓣高分", id: "doubantop"},
				{title: "动作", id: "action"},
				{title: "喜剧", id: "comedy"},
				{title: "爱情", id: "love"},
				{title: "悬疑", id: "mystery"},
				{title: "恐怖", id: "horror"},
				{title: "科幻", id: "scifi"},
				{title: "治愈", id: "sweet"},
				{title: "文艺", id: "artfilm"},
				{title: "成长", id: "youth"},
				{title: "动画", id: "animation"},
				{title: "华语", id: "chinese"},
				{title: "欧美", id: "western"},
				{title: "韩国", id: "korean"},
				{title: "日本", id: "japanese"}
			]
		}
	},
	//注册组建
	components : { MovieList },
	created() {
		this.$http
		.get("/data/movie.json")
		.then(({ data }) => {
			this.data = data;
		})
	},
	//定义方法
	methods: {
		searchValue() {
			// console.log(this.search);
			window.location.href = "http://localhost:8080/MovieHome#/MovieBroews/" + this.search;
		}
	}
}
</script>

