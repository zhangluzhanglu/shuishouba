<!-- 普通计算器 -->
<template>
	<view>
		<view class="content">{{express}}</view>
		<view class="calculator" @click="manageBtn">
			<view v-for="(item,i) in opts" :data-v="item" :key="item" :class="(i<4||['+','-','×','÷'].includes(item))?'opt':'num'">{{item}}</view>
		</view>
	</view>
</template>

<script>
	import Calculator from "./Calstack.js";
	import {
		zl_calculator_zl
	} from 'zl_calculator_zl';

	export default {
		data() {
			return {
				opts: [
					'(', ')', 'Del', 'Clear', 7, 8, 9, '+', 4, 5, 6, '-', 1, 2, 3, '×', 0, '.', '=', '÷',
				],
				express: "",
			};
		},
		methods: {
			manageBtn(e) {
				e = e || event;
				var text = e.target.dataset.v;
				if (text != undefined) {
					if (text === "=") {
						try {
							if (eval) var res = eval(this.express)
							else var res = zl_calculator_zl(this.express)
							this.express = res;
						} catch (err) {
							console.log(err);
							uni.showModal({
								content: "请输入正确的表达式！",
								showCancel: false
							})
						}
					} else if (text === "Del") {
						this.express = this.express.slice(0, -1);
					} else if (text === "Clear") {
						this.express = "";
					} else if (text === "÷") {
						this.express += "/";
					} else if (text === "×") {
						this.express += "*";
					} else this.express += text;
				}
			}
		}
	}
</script>

<style lang="scss">
	page {
		background-color: rgb(53, 53, 53);
		color: white;

		.content {
			border: 1px solid white;
			height: 60px;
			margin: 5px;
			margin-top: 20px;
			word-wrap: break-word
		}

		.opt {
			background-color: rgb(195, 191, 183);
			color: black;
		}

		.num {
			// background-color: white;
		}

		.calculator {
			display: flex;
			flex-flow: row wrap;
			height: 400px;
			align-content: space-around;
			justify-content: space-around;

			view {
				border: 1px solid white;
				border-radius: 5px;
				flex-basis: 20%;
				height: 50px;
				line-height: 50px;
				text-align: center;
			}
		}
	}
</style>
