# vue-simple-table

一个基于vuejs+webpack，简单易用的表格组件。

* 支持`列排序`。
* 支持`前端分页`，暂不支持`后端分页`。
* 需要引入`Bootstrap` css文件。

# 演示效果
## 若演示不完整或空白请直接点击[这里](http://7xswnj.com1.z0.glb.clouddn.com/simple-table.gif)

![](http://7xswnj.com1.z0.glb.clouddn.com/simple-table.gif)
<table class="table table-bordered table-striped">
    <thead>
        <tr>
            <th style="width: 100px;">name</th>
            <th style="width: 50px;">type</th>
            <th style="width: 50px;">default</th>
            <th>description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>:columns</td>
            <td>Array</td>
            <td></td>
            <td>列标题</td>
        </tr>
        <tr>
            <td>:data</td>
            <td>Array</td>
            <td></td>
            <td>数据</td>
        </tr>
        <tr>
            <td>:record</td>
            <td>Number</td>
            <td>10</td>
            <td>每页条数</td>
        </tr>
        <tr>
            <td>:sortColumn</td>
            <td>Array</td>
            <td></td>
            <td>每页条数,可选。不排序的列值为false，其他为data中相应的key 例：[false, 'date', 'temperature', 'humidity', 'rainfall', false, 'windLevel', 'pressure']</td>
        </tr>
    </tbody>
</table>

# test.vue

```
<template>
    <simple-table :columns="tableColumn" :data="tableTr" :sort-column="sortCol"></simple-table>
</template>

<script>
export default {
  data () {
      return {
        tableColumn:['站点', '时间', '气温(℃)', '湿度(%)', '雨量(ml)', '风向', '风速(级)', '气压(hPa)'],
        tableTr: data, // 格式在末尾
        sortCol: [false, 'date', 'temperature', 'humidity', 'rainfall', false, 'windLevel', 'pressure']
      }
    }
}
</script>
```

# data格式

```
"data": [{
    "name": "离岛",
    "date": "2016-08-16 15:37:48",
    "temperature": 17,
    "humidity": 23,
    "rainfall": 8,
    "windDirection": "Daniel",
    "windLevel": 3,
    "pressure": 827
  }, {
    "name": "铜陵市",
    "date": "2016-08-16 15:37:48",
    "temperature": 37,
    "humidity": 22,
    "rainfall": 15,
    "windDirection": "Helen",
    "windLevel": 2,
    "pressure": 749
  }, {
    "name": "香港岛",
    "date": "2016-08-16 15:37:48",
    "temperature": 11,
    "humidity": 22,
    "rainfall": 38,
    "windDirection": "Brenda",
    "windLevel": 9,
    "pressure": 973
  }]
```