<!-- 税收资讯 -->
<template>
	<view class="TaxInfo">
		<view class="tit">2020年个人所得税计算方式表</view>
		<view>
			<image src="../../static/images/2020-tax-method.png"></image>
		</view>
		<view class="des">
			1、工资范围在1-5000元之间的，包括5000元，适用个人所得税税率为0%;

			2、工资范围在5000-8000元之间的，包括8000元，适用个人所得税税率为3%;

			3、工资范围在8000-17000元之间的，包括17000元，适用个人所得税税率为10%;

			4、工资范围在17000-30000元之间的，包括30000元，适用个人所得税税率为20%;

			5、工资范围在30000-40000元之间的，包括40000元，适用个人所得税税率为25%;

			6、工资范围在40000-60000元之间的，包括60000元，适用个人所得税税率为30%;

			7、工资范围在60000-85000元之间的，包括85000元，适用个人所得税税率为35%;

			8、工资范围在85000元以上的，适用个人所得税税率为45%。
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	page {
		background-color: rgb(53, 53, 53);
		color: white;

	}

	.TaxInfo {
		text-align: center;
		padding-top: 20px;

		.tit {
			font-size: 20px;
		}

		image {
			margin-top: 20px;
			border: 1px solid black;
		}

		.des {
			text-align: left;
			white-space: pre-line;
			font-size: 14px;
			// border: 1px solid blue;
			margin: 30px;
			display: inline-block;
		}
	}
</style>
