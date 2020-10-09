<template>
    <div id="itemCountByWeek" style="width: 600px;height:400px;"></div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-by-week',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('itemCountByWeek'))
      bar.showLoading()
      // 指定图表的配置项和数据
      let barOption = {
        tooltip: {
          show: false
        },
        legend: {
          data: ['当天项目发布数量']
        }
      }
      bar.setOption(barOption)
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/countByWeek', response => {
        // 填入数据
        bar.setOption({
          title: {
            text: '本周项目发布数量',
            subtextStyle: {
              fontSize: 15
            }
          },
          xAxis: {type: 'category', name: '日期'},
          yAxis: {
            name: '项目发布数量',
            splitLine: {
              show: true
            }
          },
          series: [{
            name: '当天项目发布数量',
            type: 'line',
            coordinateSystem: 'cartesian2d',
            label: {
              show: true,
              position: 'top'
            }
          }],
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
