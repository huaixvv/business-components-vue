#### 远程搜索组件-基于element-ui的select组件

##### 使用方法

```javascript
  <sa-form-item label="经销商测试：" prop="test">
					<testdemo
						:value.sync="searchForm._.sel"
						:label-name="'distributorName'"
						:value-name="'distributorCode'"
						:search-fn="selectFn2"
						:search-key="'distributorName'"
					></testdemo>
				</sa-form-item>
```

> search-fn 传入ajax方法，要求promise
> label-name： select的label
> value-name：value值
> search-key：搜索要传给 search-fn 的查询字段