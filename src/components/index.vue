<template>
	<div class="index">
		<el-row>
			<el-col :span="24" style="font-size: 20px;font-weight: 500">鸣鸣哥--装修资薪预览录</el-col>
			<el-col :span="24">
				<el-table :data="list" border style="width: 100%; margin-top: 20px">
					<el-table-column prop="name0" label="自付"></el-table-column>
					<el-table-column prop="num0" label="数值（元）"></el-table-column>
					<el-table-column prop="name1" label="半包"></el-table-column>
					<el-table-column prop="num1" label="数值（元）"></el-table-column>
					<el-table-column prop="name2" label="主材"></el-table-column>
					<el-table-column prop="num2" label="数值（元）"></el-table-column>
					<el-table-column prop="name3" label="软装"></el-table-column>
					<el-table-column prop="num3" label="数值（元）"></el-table-column>
				</el-table>
			</el-col>
		</el-row>
	
	</div>
</template>

<script>
	export default {
		name: 'index',
		data() {
			return {
				list0: ['敲墙鉴定:500', '清运:1250', '敲墙+搬运:1500', '灭火器:40.8', '垃圾袋:50', '防护网:15.4'],
				list1: ['敲墙鉴定:500', '清运:1250'],
				list2: ['敲墙鉴定:500'],
				list3: ['敲墙鉴定:500'],
				list: []
			}
		},
		mounted() {
			this.list = []
			let len = Math.max(this.list0.length, this.list1.length, this.list2.length)
			for (let i = 0; i < len; i++) {
				this.list[i] = {
					name0: this.list0[i] && this.list0[i].split(':')[0],
					num0: this.list0[i] && this.list0[i].split(':')[1],
					name1: this.list1[i] && this.list1[i].split(':')[0],
					num1: this.list1[i] && this.list1[i].split(':')[1],
					name2: this.list2[i] && this.list2[i].split(':')[0],
					num2: this.list2[i] && this.list2[i].split(':')[1],
					name3: this.list3[i] && this.list3[i].split(':')[0],
					num3: this.list3[i] && this.list3[i].split(':')[1]
				}
			}
			let num0 = this.list0.map(o => Number(o.split(':')[1])).reduce((a, b) => a + b).toFixed(2)
			let num1 = this.list1.map(o => Number(o.split(':')[1])).reduce((a, b) => a + b).toFixed(2)
			let num2 = this.list2.map(o => Number(o.split(':')[1])).reduce((a, b) => a + b).toFixed(2)
			let num3 = this.list2.map(o => Number(o.split(':')[1])).reduce((a, b) => a + b).toFixed(2)
			this.list.push({name0: '合计', num0, num1, num2, num3})
			this.list.push({name0: '总计', num0: (Number(num0) + Number(num1) + Number(num2) + Number(num3)).toFixed(2)})
			this.$forceUpdate()
		},
		methods: {
			getSummaries(param) {
				const {columns, data} = param
				const sums = []
				columns.forEach((column, index) => {
					if (index === 0) {
						sums[index] = '总价'
						return
					}
					const values = data.map(item => Number(item[column.property]))
					if (!values.every(value => isNaN(value))) {
						sums[index] = values.reduce((prev, curr) => {
							const value = Number(curr)
							if (!isNaN(value)) {
								return prev + curr
							} else {
								return prev
							}
						}, 0)
						sums[index] = sums[index].toFixed(2)
						sums[index] += ' 元'
					} else {
						sums[index] = ''
					}
				})
				return sums
			}
		}
	}
</script>

<style scoped>

</style>
