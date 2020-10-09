<template>
    <div>
        <div id="countByPriceAndStatus" style="width: 600px;height:400px;"></div>
        <div id="countAllByPrice" style="width: 600px;height:400px;"></div>
    </div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-by-price',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('countByPriceAndStatus'))
      bar.showLoading()
      // 指定图表的配置项和数据
      let barOption = {
        title: {
          text: '各价格区间项目数量',
          subtextStyle: {
            fontSize: 15
          }
        },
        legend: {
          left: '30%',
          data: ['未承接', '已承接', '未完成', '已完成']
        },
        tooltip: {
          show: false
        },
        grid: [
          {bottom: '60%'},
          {top: '60%'}
        ],
        xAxis: [
          {
            type: 'category',
            name: '项目类型',
            gridIndex: 0,
            axisLabel: {
              interval: 0,
              rotate: -30
            }
          },
          {
            type: 'category',
            name: '项目类型',
            gridIndex: 1,
            axisLabel: {
              interval: 0,
              rotate: -30
            }
          }
        ],
        yAxis: [
          {
            name: '项目数量',
            gridIndex: 0
          },
          {
            name: '项目数量',
            gridIndex: 1
          }
        ],
        series: [
          {
            name: '未承接',
            type: 'bar',
            label: {
              show: true,
              position: 'top'
            }
          },
          {
            name: '已承接',
            type: 'bar',
            label: {
              show: true,
              position: 'top'
            }
          },
          {
            name: '未完成',
            type: 'bar',
            xAxisIndex: 1,
            yAxisIndex: 1,
            label: {
              show: true,
              position: 'top'
            }
          },
          {
            name: '已完成',
            type: 'bar',
            xAxisIndex: 1,
            yAxisIndex: 1,
            label: {
              show: true,
              position: 'top'
            }
          }
        ]
      }
      bar.setOption(barOption)
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams(
        '/admin/item/find/countByPriceAndStatus', response => {
          // 填入数据
          bar.setOption({
            dataset: {
              // 提供一份数据。
              source: response
            }
          })
          bar.hideLoading()
        }
      )
    },
    countDeveloperAndUser () {
      const pie = echarts.init(document.getElementById('countAllByPrice'))
      pie.showLoading()
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/countAllByPrice', response => {
        let pieOption = {
          title: {
            text: '各价格区间项目数量对比'
          },
          series: [{
            name: '各价格区间项目数量对比',
            type: 'pie',
            radius: '55%',
            label: {
              show: true,
              formatter: '{b}-{d}%'
            }
          }],
          dataset: {
            source: response
          }
        }
        pie.setOption(pieOption)
        pie.hideLoading()
      })
    }
  },
  mounted () {
    this.countDeveloper()
    this.countDeveloperAndUser()
  }
}
</script>

<style scoped>

</style>
