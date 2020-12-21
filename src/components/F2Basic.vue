<template>
  <card-base ref="cardBase">
    <canvas id="f2basic"/>
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
        id: 'f2basic',
        pixelRatio: window.devicePixelRatio, // 指定分辨率
        height: 300,
        width: this.$refs.cardBase.$el.offsetWidth - 50
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
