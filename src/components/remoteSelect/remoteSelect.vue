<template>
	<el-select
		:placeholder="placeholder"
		v-model="selected"
		:multiple="multipleCfg.multiple"
		:reserve-keyword="multipleCfg.reserveKeyword"
		filterable
		remote
		:remote-method="toRemote"
		@focus="initOptions"
		clearable
		>
		<el-option
			v-for="(item, index) in options"
			:label="item[labelName]"
			:value="item[valueName]"
			:key="item['id'] || index">
		</el-option>
	</el-select>
</template>

<script>

  export default {
    name: 'testdemo',
		props: {
      value: {
        type: String
			},
      placeholder: { // 站位
        type: String,
				default: '请输入关键词'
			},
			isMultiple: { // 是否多选
        type: Boolean,
				default: false
			},
      labelName: {
        type: String,
        default: ''
      },
      valueName: {
        type: String,
        default: ''
      },
			searchFn: { // ajax方法（promise）
        type: Function
			},
			searchKey: { // 搜索关键字
        type: String,
        default: ''
			},
			pageSize: { 
        type: Number,
        default: 20
			}
		},
		data () {
      return {
        options: [],
				current: 1
			}
		},
		computed: {
      // 多选配置
      multipleCfg () {
        return this.isMultiple ? { multiple: true, reserveKeyword: true } : { multiple: false, reserveKeyword: false }
			},
			args () {
        return {
          size: this.pageSize,
					current: this.current
				}
			},
			selected: {
        get () {
          return this.value
				},
				set (val) {
          this.$emit('update:value', val)
				}
			}
		},
		created () {
      this.initOptions()
    },
    methods: {
      // 初始化
			async initOptions () {
        this.args[this.searchKey] = ''
        let res = await this.searchFn(this.args)
        this.options = this.filterResultList(res)
			},

			// 搜索
      async query () {
        let res = await this.searchFn(this.args)
        this.options = this.filterResultList(res)
			},

      toRemote (val) {
        this.args[this.searchKey] = val
				this.query()
			},

			// 数据过滤
			filterResultList (data) {
        return Array.isArray(data) ? data : data.list
			}
		}
  }
</script>

<style scoped>

</style>
