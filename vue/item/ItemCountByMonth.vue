<template>
    <div id="itemCountByMonth" style="width: 600px;height:400px;"></div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-by-month',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('itemCountByMonth'))
      bar.showLoading()
      // 指定图表的配置项和数据
      let barOption = {
        title: {
          text: '本月项目发布数量'
        },
        tooltip: {
          show: false
        },
        legend: {
          data: ['当日项目发布数量']
        },
        xAxis: {type: 'category', name: '日期/日'},
        yAxis: {
          name: '项目发布数量',
          splitLine: {
            show: true
          }},
        series: [{
          name: '当日项目发布数量',
          type: 'line',
          label: {
            show: true,
            position: 'top'
          }
        }]
      }
      bar.setOption(barOption)
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/countByMonth', response => {
        // 填入数据
        bar.setOption({
          dataset: {
            // 提供一份数据。
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
