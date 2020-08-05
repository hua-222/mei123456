<template>
	<div>
		<Head></Head>
		<EmptyBox v-if="show"></EmptyBox>
		<CarList @JieShou="isCollect" v-else :bodys="bodys" :CollectType="false"></CarList>
	</div>
</template>

<script>
	import Head from "@/components/Head.vue"
	import EmptyBox from "@/components/EmptyBox.vue"
	import CarList from '@/components/CarList.vue'
	export default {
		name: "MyFavorite",
		components: {
			Head,
			EmptyBox,
			CarList
		},
		data() {
			return {
				show: true,
				body: undefined,
				bodys: undefined
			}
		},
		methods: {
			isCollect(id) {
				for (var i = 0; i < this.body.length; i++) {
					if (this.body[i].id == id) {
						if ((this.body[i].collect == false)) {
							this.body[i].collect = true
						} else {
							this.body[i].collect = false
						}
					}
				}
				this.bodys = this.body
				var list = this.body;
				this.bodys = list.filter(item => {
					return ((item["collect"] == true))
				})
				localStorage.setItem("cmts", JSON.stringify(list));
			},
			huoqu() {

			}
		},
		watch: {
			"bodys": function(z) {
				if (z.length == "" && z.length == 0) {
					this.show = true
				}
				else{
					this.show = false
				}

			}
		},
		mounted() {
			this.body = JSON.parse(localStorage.getItem("cmts") || "[]");
			var list = this.body;
			this.bodys = list.filter(item => {
				return ((item["collect"] == true))
			})
		}

	}
</script>

<style>
</style>
