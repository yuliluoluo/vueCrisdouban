<template>
	<!-- 只能有一个根元素 -->
<div class="music-home">
	<!-- 中国音乐 -->
	<div class="chinese">
		<div class="music-title">
			<div class="title">{{chineseSong.title}}</div>
			<router-link tag="a" :to="'/MusicList/'+chineseSong.id" class="more">更多</router-link>
		</div>
		<!-- 行列表 -->
		<div class="music-list">
			<ListPart :classify="chineseSong.id" :data="chineseList" class="list" ></ListPart>
		</div>
	</div>

	<!-- 欧美音乐 -->
	<div class="europe">
		<div class="music-title">
			<div class="title">{{europeSong.title}}</div>
			<router-link tag="a" :to="'/MusicList/'+europeSong.id" class="more">更多</router-link>
		</div>
		<!-- 行列表 -->
		<div class="music-list">
			<ListPart :classify="europeSong.id" :data="europeList" class="list" ></ListPart>
		</div>
	</div>

	<!-- 日韩音乐 -->
	<div class="jk">
		<div class="music-title">
			<div class="title">{{jkSong.title}}</div>
			<router-link tag="a" :to="'/MusicList/'+jkSong.id" class="more">更多</router-link>
		</div>
		<div class="music-list">
			<ListPart :classify="jkSong.id" :data="jkList" class="list" ></ListPart>
		</div>
	</div>				

<!-- 下面分类浏览 -->
	<!-- <div class="browse">
		<h2>分类浏览</h2>
		<ul>
			<li v-for="(item, index) in browseList" :key="index">
				<span class="browerPart">{{item.text}}</span>
				<span class="gt">&gt;</span>
	
			</li>
		</ul>
	</div> -->
	<div class="bottom-list">
        <ul>
            <li v-for="(item, index) in browseList" :key="index">
                <span>{{item.text}}</span>
                <span class="arrow">
                    <span class="arrow white"></span>
                </span>
            </li>
        </ul>
    </div>
</div>
</template>

<style type="text/css" lang="scss" scoped>
@import '../base.scss';
* {
	margin: 0;
	padding: 0;
	list-style: none;
}
.music-home a {
	text-decoration: none;
}
.music-home .green {
	color: $textColor;
}
.music-home .chinese,.europe,.jk{
	padding-left: 10px;
}
.music-home .music-title {
	width: 100%;
	display: flex;
	padding: 15px;
	color: #242424;
	box-sizing: border-box;
	font-size: 16px;
	justify-content: space-between;
	.more {
		color: $textColor;
	}
}
.music-home .music-list {
	overflow: hidden;
	height: 160px;
	width: 100%;
	/* .list {
		overflow-x: auto;
	} */
}
.music-home .bottom-list{
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
/* .browse {
	margin-top: 40px;
	color: $textColor;
	width: 100%;
	padding: 15px;
	box-sizing: border-box;
	font-size: 16px;
	h2 {
		font-size: 16px;
		color: #242424;
		line-height: 50px;
		font-weight: normal;
		border-bottom: 1px solid #EFEFEF;
	}
	ul {
		width: 100%;
		overflow: hidden;
		li {
			float: left;
			width: 50%;
			font-size: 14px;
			line-height: 40px;
			padding-right: 20px;
			box-sizing: border-box;
			height: 40px;
			display: flex;
			justify-content: space-between;
			border-bottom: 1px solid #EFEFEF;
			border-right: 1px solid #EFEFEF;
			&:nth-child(2n) {
				border-right: none;
				padding-left: 20px;
			}
			.gt {
				color: #ccc;
			}
		}
	}
} */
/* .footer {
	height: 150px;
	margin-top: 50px;
	font-size: 15px;
	text-align: center;
	.top {
		font-size: 20px;
		.dou {
			display: inline-block;
			width: 40px;
			height: 40px;
			line-height: 40px;
			border-radius: 8px;
			font-size: 24px;
			background: $textColor;
			color: #fff;
			margin-right: 5px;
			margin-bottom: 16px;
		}
	}
} */

</style>

<script type="text/javascript">
	//引入子组件,有没有办法直接引入Title子组件,在里面more的跳转路由怎么写，每个more跳转的地方不一样
	// import Title from './Item.vue';
	import ListPart from './listPart.vue';
	export default {
		// 注册子组件
		components: { ListPart },
		data() {
			return {
				chineseSong: {},
				chineseList: [],
				europeSong: {},
				europeList: [],
				jkSong: {},
				jkList: [],
				browseList: [
					{ text: '流行', id: 'popular' },
					{ text: '摇滚', id: 'rock' },
					{ text: '民谣', id: 'folk' },
					{ text: '独立', id: 'dependence' },
					{ text: '华语', id: 'chinese' },
					{ text: '欧美', id: 'western' },
					{ text: '日本', id: 'japan' },
					{ text: '韩国', id: 'korean' },
				]
			}
		},
		// 组件创建完成，请求数据
		created() {
			this.$http
			.get('/data/musicHome.json')
			.then(({data}) => {
				this.chineseSong = data.chinese;
				this.europeSong = data.europe;
				this.jkSong = data.jk;
				this.chineseList = data.chinese.list;
				this.europeList = data.europe.list;
				this.jkList = data.jk.list;

			});
		}
	}
	
</script>