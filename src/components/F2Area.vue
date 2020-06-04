<template>
  <card-base>
    <canvas class="col-12" id="containerArea" />
  </card-base>
</template>

<script>
import CardBase from 'components/CardBase'
export default {
  name: 'F2Area',
  components: {
    CardBase
  },
  data () {
    return {
      dataChart: [{
        time: '2016-08-08 00:00:00',
        tem: 10
      }, {
        time: '2016-08-08 00:10:00',
        tem: 22
      }, {
        time: '2016-08-08 00:30:00',
        tem: 16
      }, {
        time: '2016-08-09 00:35:00',
        tem: 26
      }, {
        time: '2016-08-09 01:00:00',
        tem: 12
      }, {
        time: '2016-08-09 01:20:00',
        tem: 26
      }, {
        time: '2016-08-10 01:40:00',
        tem: 18
      }, {
        time: '2016-08-10 02:00:00',
        tem: 26
      }, {
        time: '2016-08-10 02:20:00',
        tem: 12
      }]
    }
  },
  mounted () {
    this.renderChart()
  },
  methods: {
    renderChart () {
      const chart = new this.$f2.Chart({
        id: 'containerArea',
        pixelRatio: window.devicePixelRatio,
        height: 300,
        width: window.innerWidth - 50
      })

      chart.source(this.dataChart, {
        time: {
          type: 'timeCat',
          tickCount: 3,
          range: [0, 1]
        },
        tem: {
          tickCount: 5,
          min: 0
        }
      })
      chart.axis('time', {
        label: function label (text, index, total) {
          const textCfg = {}
          if (index === 0) {
            textCfg.textAlign = 'left'
          } else if (index === total - 1) {
            textCfg.textAlign = 'right'
          }
          return textCfg
        }
      })
      chart.tooltip({
        showCrosshairs: true
      })
      chart.area()
        .position('time*tem')
        .color('l(90) 0:#1890FF 1:#f7f7f7')
        .shape('smooth')
      chart.line()
        .position('time*tem')
        .color('l(90) 0:#1890FF 1:#f7f7f7')
        .shape('smooth')
      chart.render()
    }
  }
}
</script>
