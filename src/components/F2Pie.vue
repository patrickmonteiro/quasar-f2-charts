<template>
  <card-base>
    <canvas class="col-12" id="containerPie" />
  </card-base>
</template>

<script>
import CardBase from 'components/CardBase'
export default {
  name: 'F2Pie',
  components: {
    CardBase
  },
  data () {
    return {
      map: {
        Fanghua: '40%',
        Legend: '20%',
        Machine: '18%',
        Psychological: '15%',
        Dream: '5%',
        Other: '2%'
      },
      dataChart: [{
        name: 'Fanghua',
        percent: 0.4,
        a: '1'
      }, {
        name: 'Legend',
        percent: 0.2,
        a: '1'
      }, {
        name: 'Machine',
        percent: 0.18,
        a: '1'
      }, {
        name: 'Psychological',
        percent: 0.15,
        a: '1'
      }, {
        name: 'Dream',
        percent: 0.05,
        a: '1'
      }, {
        name: 'Other',
        percent: 0.02,
        a: '1'
      }]
    }
  },
  mounted () {
    this.renderChart()
  },
  methods: {
    renderChart () {
      const chart = new this.$f2.Chart({
        id: 'containerPie',
        pixelRatio: window.devicePixelRatio,
        height: 300,
        width: window.innerWidth - 50
      })
      chart.source(this.dataChart, {
        percent: {
          formatter: function formatter (val) {
            return val * 100 + '%'
          }
        }
      })
      chart.legend({
        position: 'right',
        itemFormatter: (val) => val + '  ' + this.map[val]

      })
      chart.tooltip(false)
      chart.coord('polar', {
        transposed: true,
        radius: 0.85
      })
      chart.axis(false)
      chart.interval()
        .position('a*percent')
        .color('name', ['#1890FF', '#13C2C2', '#2FC25B', '#FACC14', '#F04864', '#8543E0'])
        .adjust('stack')
        .style({
          lineWidth: 1,
          stroke: '#fff',
          lineJoin: 'round',
          lineCap: 'round'
        })
        .animate({
          appear: {
            duration: 1200,
            easing: 'bounceOut'
          }
        })

      chart.render()
    }
  }
}
</script>
