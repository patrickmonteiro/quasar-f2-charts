<template>
  <card-base>
    <canvas class="col-12" id="container"/>
  </card-base>
</template>

<script>
import CardBase from 'components/CardBase'
export default {
  name: 'F2Basic',
  components: {
    CardBase
  },
  data () {
    return {
      dataChart: [
        { genre: 'Sports', sold: 275 },
        { genre: 'Strategy', sold: 115 },
        { genre: 'Action', sold: 120 },
        { genre: 'Shooter', sold: 350 },
        { genre: 'Other', sold: 150 }
      ]
    }
  },
  mounted () {
    this.renderChart()
  },
  methods: {
    renderChart () {
      const chart = new this.$f2.Chart({
        id: 'container',
        pixelRatio: window.devicePixelRatio, // 指定分辨率
        height: 300,
        width: window.innerWidth - 50
      })

      chart.source(this.dataChart)

      chart.interval()
        .position('genre*sold')
        .color('genre')

      chart.render()
    }
  }
}
</script>
