<!-- 个人所得税计算 -->
<template>
	<view class="taxCal">
		<form @submit="formSubmit">
			<view>
				<label>税前总收入:</label><input value="0" type="digit" name="taxbefore" />
			</view>
			<view>
				<label>五险一金支出:</label><input value="0" type="digit" name="fivexyj" />
			</view>
			<view>
				<label>专项扣除:</label><input value="0" type="digit" name="zx" />
			</view>
			<view>
				<label>其他支出:</label><input value="0" type="digit" name="other" />
			</view>
			<view>
				<button size="mini" form-type="submit" plain="true">计算</button>
			</view>
		</form>
		<view>
			计算结果:
			<ul>
				<li>需要缴税：{{taxM}} 元</li>
				<li>税后收入：{{mongAfterTax}} 元</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
                taxM:0, //需要缴税
				mongAfterTax:0,//税后收入
				
			};
		},
		methods: {
			formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' ,e.detail.value)
				var formdata = e.detail.value
				//当月减去支出后的收入
				var allMoney = formdata.taxbefore - formdata.fivexyj - formdata.zx - formdata.other
				//当月净收入扣税
				var taxMoney = this.getTax(allMoney);
				//当月实际收入为
				var currentMonthMoney = allMoney - taxMoney;
				//将结果显示在页面上
				this.taxM=taxMoney;
				this.mongAfterTax=currentMonthMoney;
				
				// uni.showModal({
				// 	content: '表单数据内容：' + taxMoney,
				// 	showCancel: false
				// });
			},
			getTax(allMoney) {
				var tax = 0;
				if (allMoney <= 5000) tax = 0;
				else if (allMoney <= 8000) tax = (allMoney - 5000) * 0.03;
				else if (allMoney <= 17000) tax = 90 + (allMoney - 8000) * 0.1;
				else if (allMoney <= 30000) tax = 90 + 900 + (allMoney - 17000) * 0.2;
				else if (allMoney <= 40000) tax = 90 + 900 + 2600 + (allMoney - 30000) * 0.25;
				else if (allMoney <= 60000) tax = 90 + 900 + 2600 + 2500 + (allMoney - 40000) * 0.3;
				else if (allMoney <= 85000) tax = 90 + 900 + 2600 + 2500 + 6000 + (allMoney - 60000) * 0.35;
				else tax = 90 + 900 + 2600 + 2500 + 6000 + 8750 + (allMoney - 85000) * 0.45;
				return tax;
			}
		}
	}
</script>

<style lang="scss">
	page {
		background-color: rgb(43, 40, 40);
		font-size: 16px; //让其符号大小在不同设备上保存一致
	}

	.taxCal {
		&>view {
			margin: 5px;
			margin-top: 80px;
			border-radius: 5px;
			border: 1rpx solid white;
			ul li{
				margin:5px;
			}
		}
		

		color: white;

		form {
			view {
				margin: 10px;

				input {
					box-shadow: 0 0 5px white;
					padding-left: 5px;
					height: 30px;
				}

				label {
					font-size: 14px;
					display: inline-block;
					padding: 10px;
				}
			}

			button {
				color: white;
				height: 30px;
				float: right;
				width: 80px;
				height: 40px;
				line-height: 40px;
				font-weight: bold;
				font-size: 16px;
			}
		}

	}
</style>
