<template>
<!-- <div class="wrapper">
	<ul class="count">
		<li v-for="(item, index) in data" :key="index">
			<router-link class="item" tag="div" :to="'/MovieDetail/' + item.id" :data="item.id">
				<img :src="item.cover.url" alt="">
				<p>{{item.title}}</p>
				<div class="rate">
					<el-rate  disabled v-model="item.rating.value"></el-rate>
					<span>{{item.rating.value * 2}}</span>
				</div>
			</router-link>
		</li>
	</ul>
</div> -->
 <div class="wrapper" >
                <ul class="content">
                    <li v-for="(item,index) in data" @click="fun_detail(item.id)" :key="index">
                        <img :src="item.cover.url" alt="">
                        <p>{{item.title}}</p>
                        <div class="stars-container">
                            <div id="stars">
                              <span v-for="(i, index) in item.stars" :key="index">
                                <img v-if="i" src="/img/book/star.png" >
                                <img v-else src="/img/book/none-star.png" >
                              </span>
                             </div>
                            <div :class="item.rating==0?'starScoreNull':'starScore'">{{item.rating.value*2}}</div>
                        </div>
                    </li>
                </ul>
            </div>
</template>
<!-- 样式 -->
<style type="text/css" lang="scss" scoped>
.wrapper{
        width: 100%;
        height: 200px;
        padding: 10px 10px;
        /* position: relative;
        left: 0;
        top: 0; */
        overflow: hidden;
        .content{
            white-space: nowrap;
            width: 100%;
            height: 236px;
            overflow-x:auto;
            overflow-y:hidden; 
        }
            li{
            display: inline-block;
            margin-right: 6px;
            width: 100px;
            height: 150px;
            list-style: none;
            text-align: center;
            img{
                height: 90%;
                width:100%;
            }
            p{
                    font-size: 14px;                
                    overflow: hidden;
                    white-space: nowrap;
                    text-overflow: ellipsis;
                    color: #111;
                    span{
                        color: #aaa;
                    }
            }
            .starScore{
              color: #ea2000;
              font-size: 12px;
                }
            .starScoreNull{
                font-size: 12px;
                }
            .stars-container {
                height: 20px;
                display: flex;
                padding: 0 5px;
                flex-direction: row;
                align-items:center;
                justify-content:space-between;
                    #stars img {
                    padding-left: 3rpx;
                    height: 12px;
                    width: 12px;
                    }
                }
        }
        
    }
/* .wrapper{
	width: 100%;
        height: 200px;
        padding: 10px 0;
        overflow: hidden;
}
.count {
	list-style: none;
	width: 100%;
	overflow-x: auto;
	overflow-y:hidden;
	height: 236px;
	white-space: nowrap;
	li {
		div{

			width: 100%;
			height: 100%;
		}
		display: inline-block;
		width: 100px;
		height: 150px;
		margin-right: 6px;
		img {
			height: 90%;
		}
		p {
			width: 100%;
			line-height: 30px;
			text-align: center;
			font-size: 14px;
			color: #111;
			white-space: nowrap;
			text-overflow: ellipsis;
			overflow: hidden;
		}
		.rate {
			display: flex;
			width: 100%;
			el-rate {
				flex: 8;
			}
			span {
				flex: 1;
				width: 20%;
				color: #999;
				font-size: 14px;
			}
		}
	}
} */
</style>
<script type="text/javascript">
export default {
	props : ["data"],
	created() {
		// console.log(this.data);
		var newarr = Array.from(this.data);
		// var newdata = {};
		// console.log(newdata);
		for(var i = 0; i<newarr.length; i++) {
			newarr[i].rating.value = newarr[i].rating.value / 2;
            let r=Math.round(newarr[i].rating.value);
                            let arr=[0,0,0,0,0];
                            let index=0;
                            while(r){
                                arr[index]=1;
                                r--;
                                index++;
                            }
                            newarr[i].stars=arr;
		}
	},
	methods:{
		fun_detail(id){
                this.$router.push('/MovieDetail/'+id);
            }
	}
}
</script>