<template>
	<div>
		<Head></Head>
		<div class="TouBu">
			<div class="banner TouBu-top">
				<mt-swipe :auto="0" ref="swipe" :show-indicators="false" @change="swipeChange()">
					<mt-swipe-item v-for="item in body[0].imgurl.bigurl" :key="item"><img :src="item" alt=""></mt-swipe-item>

				</mt-swipe>
				<div class="xianshi">
					<img src="../assets/picture-icon.png" alt="">
					<span><input v-model="activeIndex">/{{pagesLength}}</span>
				</div>
			</div>
			<div class="TouBu-but">
				<span>陆风X7 2015款 2.0T 全景尊贵版</span>
				<div class="jiage">
					<div>
						<span>6.25</span>
						<span>万</span>
					</div>
					<span>12人关注</span>
				</div>

			</div>
		</div>
		<div class="JiBenXinXi">
			<span>基本信息</span>
			<div class="JiBenXinXi-top">
				<div class="JiBenXinXi-top-li">
					<span>车驾龄</span>
					<p>{{body[0].DrivingYears}}年</p>
				</div>
				<div class="JiBenXinXi-top-li">
					<span>行驶里程</span>
					<p>{{body[0].ActualServiceLife|PriceFormat("万公里")}}</p>
				</div>
			</div>
			<div class="JiBenXinXi-but">
				<router-link to="">查看车辆详细信息</router-link>
			</div>
		</div>

		<div class="mains">
			<div class="recomm">
				<div class="host" style="border-bottom:0;">
					<h4>为您推荐</h4>
					<router-link to="/BuyCars">
						更多 <i class="el-icon-arrow-right"></i>
					</router-link>
				</div>
			</div>
		</div>
		<CarListTJ :bodys="bodys"></CarListTJ>
	</div>
</template>

<script>
	import Head from '@/components/Head.vue'
	import CarListTJ from '@/components/CarListTJ.vue'
	export default {
		name: "CarIntroduced",
		components: {
			Head,
			CarListTJ
		},
		data() {
			return {
				activeIndex: 1,
				pagesLength: 1,
				bodys: "",
				body: ""
			}
		},
		methods: {
			swipeChange() {
				this.activeIndex = this.$refs.swipe.index + 1;
			},
		},
		created() {
			let bodys = this.$route.query.bodys;
			let id = this.$route.query.id;
			this.bodys = bodys;
			this.body = bodys.filter(item => {
				return (item["id"] == id)
			});
			this.pagesLength = this.body[0].imgurl.bigurl.length

		}


	}
</script>

<style>
	.TouBu-top {
		position: relative;
		height: 15.625rem;
	}

	.xianshi {
		position: absolute;
		top: 220px;
		left: 15px;
		display: flex;
		background-color: rgba(0, 0, 0, .4);
		width: 53px;
		height: 20px;
		justify-content: center;
		align-items: center;
	}

	.xianshi img {
		width: 1.0625rem;
		height: 1.0625rem;
	}

	.xianshi span {
		font-size: 0.8125rem;
		color: #FFFFFF;
	}

	.xianshi input {
		background: none;
		color: #FFFFFF;
		text-align: center;
		width: 15px;
	}

	.TouBu-but {
		padding: 0.625rem 15px 10px;
		display: flex;
		flex-direction: column;
		border-bottom: 10px solid #f5f7fa;
	}

	.TouBu-but span {
		color: #495056;
		line-height: 30px;
	}

	.TouBu-but .jiage {
		display: flex;
		justify-content: space-between;
	}

	.TouBu-but .jiage span:nth-child(1) {
		color: #ff7147;
		font-size: 22px;
	}

	.TouBu-but .jiage span:nth-child(2) {
		color: #ff7147;
		font-size: 16px;
	}

	.JiBenXinXi {
		padding: 0.625rem 15px 10px;
		border-bottom: 10px solid #f5f7fa;
		position: relative;
	}

	.JiBenXinXi span:nth-child(1) {
		color: #495056;
		line-height: 30px;
	}

	.JiBenXinXi-top {
		display: flex;
		justify-content: space-between;
	}

	.JiBenXinXi-top-li {
		display: flex;
		flex-direction: column;

	}

	.JiBenXinXi-top .JiBenXinXi-top-li span {
		line-height: 1.4375rem;
		color: #abafb3;
	}

	.JiBenXinXi-but {
		width: 100%;
	}

	.JiBenXinXi-but a {
		display: block;
		color: #757f89;
		width: 80%;
		border-radius: 0.1875rem;
		text-align: center;
		font-size: 14px;
		line-height: 34px;
		left: 9%;
		position: relative;
		border: 1px solid #abafb3;
		margin-top: 1.625rem;
	}
</style>
