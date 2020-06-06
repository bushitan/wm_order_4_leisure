<template>
		<view class="bg-white">
			<view class="flex justify-center">
				<image src="../../static/images/strong/1.png" mode="widthFix" style="width: 60vw;"></image>
			</view>
			<view class="flex justify-center">
				<image src="../../static/images/strong/slogan.png" mode="widthFix" style="width: 100vw;"></image>
			</view>
		<!-- 	<view class="flex justify-center padding-lr">
				<image src="../../static/images/strong/banner.jpg" mode="widthFix" style="width:100%"></image>
			</view> -->
			
		<!-- 	<view class="zaiui-view-content">
				<view class="zaiui-swiper-box">
					<swiper class="screen-swiper square-dot c" autoplay circular indicator-dots :current="swiperInfo.index"  @change="swiperChange">
						<swiper-item v-for="(item,index) in swiperInfo.list" :key="index">
							<view class="swiper-padding">
								<image :src="item.swiper" mode="widthFix"/>
							</view>
						</swiper-item>
					</swiper>
				</view>
			</view> -->
			
			
			<swiper class="card-swiper square-dot" indicator-dots="true" circular="true" autoplay="true" interval="5000" duration="500" bindchange="cardSwiper" indicator-color="#8799a3" indicator-active-color="#000000">
			  <swiper-item v-for="(item,index) in swiperInfo.list" :key="index" :class="cardCur==index?'cur':''">
			    <view class="swiper-item">
			      <image :src="item.swiper" mode="aspectFill"  ></image>
			    </view>
			  </swiper-item>
			</swiper>
			
			<view class="cu-bar bg-white ">
				  <view class='action'>
					<text class='cuIcon-titles text-black '></text>产品列表
				  </view>
				 <!-- <view class='action'>
					<switch class='sm' checked='{{isCard}}' bindchange='isCard'></switch>
				  </view> -->
			</view>
			
			<view class="cu-card case no-card">
				<view class="cu-item ">
					<view class="image shadow shadow-warp">
						  <image src="../../static/images/strong/good_1.jpg" mode="aspectFill" style="height: 150px;"></image>
						  <view class="cu-tag bg-red">分销10元奖励</view>
						  <view class="cu-bar bg-shadeBottom">
							<text class="text-cut">桂花冰酿</text>
						  </view>
					</view>
					<!-- <view class="cu-list menu-avatar padding-lr">
						  <view class="cu-item">
							<view class=" flex-sub">
							  <view class="text-black ">桂花冰酿</view>
							  <view class="text-gray  text-sm flex justify-between">
								每天限量
							  </view>
							</view>
						  </view>
					</view> -->
				</view>			
			</view>
			
			
			<view class="cu-card case no-card">
				<view class="cu-item ">
					<view class="image shadow shadow-warp">
						  <image src="../../static/images/strong/good_2.jpg" mode="aspectFill" style="height: 150px;"></image>
						  <view class="cu-tag bg-red">分销10元奖励</view>
						  <view class="cu-bar bg-shadeBottom">
							<text class="text-cut">招牌冰滴</text>
						  </view>
					</view>
					<!-- <view class="cu-list menu-avatar padding-lr">
						  <view class="cu-item">
							<view class=" flex-sub">
							  <view class="text-black ">桂花冰酿</view>
							  <view class="text-gray  text-sm flex justify-between">
								每天限量
							  </view>
							</view>
						  </view>
					</view> -->
				</view>			
			</view>
			
			<view class="text-center text-gray text-xs margin-top-xl">
				这是底部
			</view>
			<view class="pg-space-xl">
				
			</view>
			
		</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				isHost: true,
				isSeller: true,
				daystats: { totalScore: 0, totalPrize:0}, // 今日数据
					swiperList:[
						"/static/images/strong/swiper1_lg.jpg",
						"/static/images/strong/swiper2_lg.jpg",
					],
				storeList:[
					{name:"康浦店",id:1,url:"/static/images/strong/store_1.png"},
					{name:"盛天地店",id:7,url:"/static/images/strong/store_2.png"},
					{name:"南湖店",id:6,url:"/static/images/strong/store_3.png"},
				],
				store:{},
				orderList:[], //订单列表
				
				
				
				swiperInfo: {index: 0, show: true, welcome: true, 
					list: [
						
							{
								swiper: '../../static/images/strong/banner.jpg',
								background: '/static/images/home/swiper/swiper-background-1.png',
							},
							{
								swiper: '../../static/images/strong/banner.jpg',
								background: '/static/images/home/swiper/swiper-background-2.png',
							},
							{
								swiper: '../../static/images/strong/banner.jpg',
								background: '/static/images/home/swiper/swiper-background-3.png',
							}
					]},
				
			}
		},
		onLoad() {
			this.onInit()
		},
		onShareAppMessage() {
			
		},
		methods: {
			
			async onInit(){		
				var res = await this.db.orderGetList({
					Page:1,
					Limit:15,				
					CreatedAtMin: this.today,
					
				})	
				this.setData({
					orderList:res.data
				})
			},
			toMenu(id,name){
				uni.setStorageSync(this.db.KEY_SHOP_ID,id)
				uni.setStorageSync(this.db.KEY_SHOP_NAME,name)
				uni.switchTab({
					url:"/pages/menu/menu"
				})				
			},			
			toOrder(){
				uni.navigateTo({
					url:"/pages/order/list"
				})
			},
			toDetail(){
				var shop = this.$data.storeList[0]				
				uni.setStorageSync(this.db.KEY_SHOP_ID,shop.id)
				uni.setStorageSync(this.db.KEY_SHOP_NAME,shop.name)
				uni.switchTab({
					url:"/pages/order/current"
				})
				
			},
			
			swiperChange(){
				
			},
		}
	}
</script>

<style lang="scss" scoped>
	
	page{
	    background-color: var(--white)
	}
	
	
	
	.zaiui-view-content {
		// display: none;
		width: 100%;		
		.zaiui-tab-list {
			position: relative;
			width: 100%;
		}
	}
	.zaiui-view-content.welcome {
		/* #ifdef APP-PLUS */
		margin-top: calc(var(--status-bar-height) + 180rpx);
		/* #endif */
		
		/* #ifdef H5 */
		margin-top: calc(var(--status-bar-height) + 220rpx);
		/* #endif */
		
		/* #ifdef MP */
		margin-top: calc(var(--status-bar-height) + 220rpx);
		/* #endif */
		
		transition: all .25s;
	}
	.zaiui-view-content.show {
		display: block;
	}
</style>
