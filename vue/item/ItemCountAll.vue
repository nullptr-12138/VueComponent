<template>
    <div>
        <div id="itemCountStatus" style="width: 600px;height:400px;"></div>
        <div id="itemCountAll" style="width: 600px;height:400px;"></div>
    </div>
</template>

<script>
import echarts from 'echarts'
import HttpRequestUtils from '../../../assets/js/HttpRequestUtils'

export default {
  name: 'item-count-all',
  methods: {
    countDeveloperAndUser () {
      const pie1 = echarts.init(document.getElementById('itemCountStatus'))
      const pie2 = echarts.init(document.getElementById('itemCountAll'))
      pie1.showLoading()
      pie2.showLoading()
      // 异步加载数据
      HttpRequestUtils.doGetWithoutParams('/admin/item/find/countAll', response => {
        let pieOption1 = {
          title: {
            text: '项目完成数量对比',
            subtext: '总项目发布数量为:' + response.all,
            subtextStyle: {
              fontSize: 15
            }
          },
          series: [{
            name: '项目完成量对比',
            type: 'pie',
            radius: '55%',
            label: {
              show: true,
              formatter: '{b}-{d}%'
            },
            data: [
              {value: response.statusIsFalse, name: '未完成项目'},
              {value: response.statusIsTrue, name: '已完成项目'}
            ]
          }]
        }
        let pieOption2 = {
          series: [{
            name: '项目承接量对比',
            type: 'pie',
            radius: '55%',
            label: {
              show: true,
              formatter: '{b}-{d}%'
            },
            data: [
              {value: response.all - response.developer, name: '未承接项目'},
              {value: response.developer, name: '已被承接项目'}
            ]
          }]
        }
        pie1.setOption(pieOption1)
        pie1.hideLoading()
        pie2.setOption(pieOption2)
        pie2.hideLoading()
      })
    }
  },
  mounted () {
    this.countDeveloperAndUser()
  }
}
</script>

<style scoped>

</style>
