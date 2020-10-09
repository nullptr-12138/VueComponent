<template>
    <div id="itemAvgPrice" style="width: 600px;height:400px;"></div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-avg-price',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('itemAvgPrice'))
      bar.showLoading()
      // 指定图表的配置项和数据
      let barOption = {
        tooltip: {
          show: false
        },
        legend: {
          data: ['该类型项目平均价格']
        },
        grid: {
          top: '25%'
        },
        xAxis: {type: 'category', name: '等级'},
        yAxis: {name: '平均价格'},
        series: [{
          name: '该类型项目平均价格',
          type: 'bar',
          label: {
            show: true,
            position: 'top'
          }
        }]
      }
      bar.setOption(barOption)
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/avgPriceByType', response => {
        // 填入数据
        bar.setOption({
          title: {
            text: '各类型项目平均价格'
          },
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
