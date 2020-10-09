<template>
  <div>
    <div id="itemCountByTypeAndStatus" style="width:600px;height:400px;"></div>
    <div id="itemCountAllByType" style="width:600px;height:400px;"></div>
  </div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-by-type',
  methods: {
    countDeveloper () {
      const bar = echarts.init(document.getElementById('itemCountByTypeAndStatus'))
      bar.showLoading()
      // 指定图表的配置项和数据
      let barOption = {
        title: {
          text: '各类型项目数量',
          subtextStyle: {
            fontSize: 15
          }
        },
        legend: {
          data: ['未承接', '已承接', '已完成', '未完成']
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
        '/admin/item/find/countByTypeAndStatus', response => {
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
      const pie = echarts.init(document.getElementById('itemCountAllByType'))
      pie.showLoading()
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams(
        '/admin/item/find/countAllByType',
        response => {
          let pieOption = {
            title: {
              text: '各类型项目数量对比'
            },
            series: [
              {
                name: '各种类型项目发布数量对比',
                type: 'pie',
                radius: '55%',
                label: {
                  show: true,
                  formatter: '{b}-{d}%'
                }
              }],
            dataset: {
              // 提供一份数据。
              source: response
            }
          }
          pie.setOption(pieOption)
          pie.hideLoading()
        }
      )
    }
  },
  mounted () {
    this.countDeveloper()
    this.countDeveloperAndUser()
  }
}
</script>

<style scoped></style>
