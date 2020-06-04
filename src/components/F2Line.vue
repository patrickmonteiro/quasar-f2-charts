<template>
  <card-base>
    <canvas class="col-12" id="containerLine" />
  </card-base>
</template>

<script>
import CardBase from 'components/CardBase'
export default {
  name: 'F2Line',
  components: {
    CardBase
  },
  data () {
    return {
      dataChart: [
        {
          day: 'Mon',
          value: 300
        },
        {
          day: 'Tue',
          value: 400
        },
        {
          day: 'Wed',
          value: 350
        },
        {
          day: 'Thu',
          value: 500
        },
        {
          day: 'Fri',
          value: 490
        },
        {
          day: 'Sat',
          value: 600
        },
        {
          day: 'Sun',
          value: 900
        }
      ]
    }
  },
  mounted () {
    this.renderChart()
  },
  methods: {
    renderChart () {
      const chart = new this.$f2.Chart({
        id: 'containerLine',
        pixelRatio: window.devicePixelRatio,
        height: 300,
        width: window.innerWidth - 50
      })

      chart.source(this.dataChart, {
        value: {
          tickCount: 5,
          min: 0
        },
        day: {
          range: [0, 1]
        }
      })
      chart.tooltip({
        showCrosshairs: true,
        showItemMarker: false,
        onShow: function onShow (ev) {
          const items = ev.items
          items[0].name = null
          items[0].value = '$ ' + items[0].value
        }
      })
      chart.axis('day', {
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
      chart.line().position('day*value')
      chart
        .point()
        .position('day*value')
        .style({
          stroke: '#fff',
          lineWidth: 1
        })
      chart.render()
    }
  }
}
</script>
