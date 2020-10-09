<template>
    <div id="itemCountByYear" style="width: 600px;height:400px;"></div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-by-year',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('itemCountByYear'))
      bar.showLoading()
      // 指定图表的配置项和数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/countByYear', response => {
        // 填入数据
        bar.setOption({
          title: {
            text: '本年度项目发布数量变化图'
          },
          legend: {
            data: ['当月项目发布数量']
          },
          xAxis: {
            type: 'category', name: '月份'
          },
          yAxis: {
            name: '项目发布数量',
            splitLine: {
              show: true
            }
          },
          series: [{
            name: '当月项目发布数量',
            type: 'line',
            coordinateSystem: 'cartesian2d',
            label: {
              show: true,
              position: 'top'
            }
          }],
          dataset: {
            source: response
          }
        })
        bar.hideLoading()
      })
    }
  },
  mounted () {
    this.countDeveloper()
  }
}
</script>

<style scoped>

</style>
