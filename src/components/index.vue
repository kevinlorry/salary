<template>
	<div class="index">
		<el-table
				:data="tableData"
				border
				height="200"
				:summary-method="getSummaries"
				show-summary
				style="width: 100%; margin-top: 20px">
			<el-table-column
					prop="id"
					label="ID"
					width="180">
			</el-table-column>
			<el-table-column
					prop="name"
					label="姓名">
			</el-table-column>
			<el-table-column
					prop="amount1"
					label="数值 1（元）">
			</el-table-column>
			<el-table-column
					prop="amount2"
					label="数值 2（元）">
			</el-table-column>
			<el-table-column
					prop="amount3"
					label="数值 3（元）">
			</el-table-column>
		</el-table>
	</div>
</template>

<script>
	export default {
		name: 'index',
		data() {
			return {
				list0:['敲墙鉴定:500','清运:1250','敲墙+搬运:1500','灭火器:40.8','垃圾袋:50','防护网:15.4'],
				list1:[],
				list2:[],
				list: []
			}
		},
		mounted(){
			
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
						sums[index] += ' 元'
					} else {
						sums[index] = 'N/A'
					}
				})
				return sums
			}
		}
	}
</script>

<style scoped>

</style>
