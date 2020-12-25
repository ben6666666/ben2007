<template>
	<view>
		<view >
			列表页面
		</view>
		<button @click="pullDown">下拉刷新</button>
		<button type="default" @click="getData">请求数据</button>
		<button type="default" @click="setStorage">存储数据</button>
		<button type="default" @click="getStorage">获取数据</button>
		<button type="default" @click="removeStorage">移除数据</button>
		<view v-for="item in list" class="list">
			{{item}}
		</view>
		
	</view>
</template>

<script>
	export default{
		data(){
			return{
				list:[1 ,2 ,3 , 4 ,5 ,6 ,7 ,8],
			}
		},
		//下拉刷新函数 配合"enablePullDownRefresh":true使用
		onPullDownRefresh(){
			setTimeout(() =>{
				this.list = [4 ,3 , 2, 1];
			//停止刷新
			uni.stopPullDownRefresh();
			},2000)
			
		},
		onReachBottom(){
			console.log("滚动成功");
			this.list = [...this.list,...[4 ,3 , 2, 1]]
		},
		
		methods:{
			pullDown(){
				//监听下拉刷新事件
				uni.startPullDownRefresh()
			},
			getData(){
				uni.request({
					url:'http://localhost:3000/cartList',
					success(res) {
						console.log(res)
					}
				})
			},
			setStorage(){
				// uni.setStorage({
				// 	key:"id",
				// 	data:80,
				// 	success() {
				// 		console.log("存储成功")
				// 	}
				// })
				uni.setStorageSync("id",100)
			},
			getStorage(){
				// uni.getStorage({
				// 	key:"id",
				// 	success(res) {
				// 		console.log("获取成功",res)
				// 	}
				// })
				console.log(uni.getStorageSync("id"))
			},
			removeStorage(){
				// uni.removeStorage({
				// 	key:"id",
				// 	success() {
				// 		console.log("移除成功")
				// 	}
				// })
				uni.removeStorageSync("id")
			}
		}
	}
</script>

<style>
	.list{
		height: 100px;
		width: 100%;
	}
</style>
