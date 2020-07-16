<template>
  <div class="big">
    <div class="title">
      <span></span>
      {{title}}
      <span></span>
    </div>
    <div class="neweight" ref="neweight">neweight</div>
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  data () {
    return {
      title: '景区住宿接待情况'
    }
  },
  mounted () {
    const neweight = this.$echarts.init(this.$refs.neweight)
    const echartData = [
      { value: 34, name: '旅馆' },
      { value: 30, name: '一星酒店' },
      { value: 25, name: '二星酒店' },
      { value: 20, name: '三星酒店' },
      { value: 15, name: '四星酒店' },
      { value: 10, name: '五星酒店' }
    ]
    let total = 0
    echartData.forEach(item => {
      total += item.value
    })

    const option = {
      color: [
        new echarts.graphic.LinearGradient(
          0, 0, 0, 1,
          [
            { offset: 0, color: '#0fd4f9' },
            { offset: 1, color: '#0488ed' }
          ]
        ),
        new echarts.graphic.LinearGradient(
          0, 0, 0, 1,
          [
            { offset: 0, color: '#0573ea' },
            { offset: 1, color: '#0487ed' }
          ]
        ),
        new echarts.graphic.LinearGradient(
          0, 0, 0, 1,
          [
            { offset: 0, color: '#13bdb4' },
            { offset: 1, color: '#12bcb2' }
          ]
        ),

        new echarts.graphic.LinearGradient(
          0, 0, 0, 1,
          [
            { offset: 0, color: '#ffcc5e' },
            { offset: 1, color: '#ffc755' }
          ]
        ),

        new echarts.graphic.LinearGradient(
          0, 0, 0, 1,
          [
            { offset: 0, color: '#ff3672' },
            { offset: 1, color: '#ff326c' }
          ]
        ), '#ff0000'],

      tooltip: {
        trigger: 'item',
        textStyle: {
          fontSize: 14
        },
        formatter: '{b} : {c} ({d}%)'
      },
      legend: {
        show: false,
        icon: 'rect',
        itemWidth: 8,
        itemHeight: 8,
        orient: 'vertical',
        right: 20,
        top: '25%',
        textStyle: {
          color: '#e9e9ea',
          fontSize: 14
        },
        formatter: function (name) {
          let res = echartData.filter(v => v.name === name)
          res = res[0]
          const percent = (res.value * 100 / total).toFixed(2)
          return '  ' + name + '  ' + percent + '%'
        }
        // data: ['阳明山国家森林公园', '阳明博物馆', '上堡客家梯田', '君子谷野果世界', '聂都溶洞', '齐云山国家级自然保护区', '阳明湖国家湿地公园1', '阳明湖国家湿地公园2', '阳明湖国家湿地公园3']
      },
      calculable: true,
      series: [
        { // 内环
          type: 'pie',
          radius: ['20%', '16%'],
          center: ['50%', '50%'],
          hoverAnimation: false,
          labelLine: {
            normal: {
              show: false
            },
            emphasis: {
              show: false
            }
          },
          data: [{
            name: '',
            value: 0,
            itemStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0, 0, 0, 1,
                  [
                    { offset: 0, color: '#fafeff' },
                    { offset: 1, color: '#71dbf5' }
                  ]
                )
              }
            }
          }]
        },
        {
          type: 'pie',
          radius: ['30%', '60%'],
          center: ['50%', '50%'],
          roseType: 'radius',
          avoidLabelOverlap: true,
          zlevel: 10,
          label: {
            formatter: '{b}%\n{hr|}\n{c}人次（{d}%）',
            alignTo: 'labelLine',
            distanceToLabelLine: 0,
            bleedMargin: 10,
            align: 'left',
            verticalAlign: 'top',
            rich: {
              hr: {
                height: 0,
                borderWidth: 1,
                width: '70%',
                borderColor: '#fff'
              },
              c: {
                position: [-20, 0]
              }
            },
            fontSize: 16,
            lineHeight: 14,
            color: '#fff',
            fontWeight: 'normal'
          },
          labelLine: {
            length2: 30,
            lineStyle: {
              color: '#ffffff',
              width: 1
            }
          },
          data: echartData
        }]
    }
    neweight.setOption(option)
    window.addEventListener('resize', function () {
      neweight.resize()
    })
  }
}
</script>

<style scoped lang="less">
.big {
  width: 600px;
  height: 400px;
  border-top: 3px solid #00f5fc;
  background-color: #0a1f39;
  position: relative;
  .title {
    width: 200px;
    height: 40px;
    line-height: 40px;
    color: #fff;
    font-weight: 700;
    letter-spacing: 3px;
    background-image: linear-gradient(#0b58b799, #0e8dba);
    position: absolute;
    top: -3px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 2;
    display: flex;
    justify-content: space-between;
    span {
      display: block;
      width: 0;
      height: 0;
      border-width: 10px;
      border-color: #0a1f39;
    }
  }
}
.neweight {
  width: 600px;
  height: 360px;
}
</style>
