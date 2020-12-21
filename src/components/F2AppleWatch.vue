<template>
  <card-base ref="cardBase">
    <canvas id="f2Guage"/>
  </card-base>
</template>

<script>
import CardBase from 'components/CardBase'
import { Util } from '@antv/f2'

export default {
  name: 'f2Guage',
  components: {
    CardBase
  },
  data () {
    return {
      dataChart: [
        {
          const: 'a',
          actual: 90,
          expect: 100
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
        id: 'f2Guage',
        pixelRatio: window.devicePixelRatio, // 指定分辨率
        height: 300,
        padding: [0, 30, 60],
        width: this.$refs.cardBase.$el.offsetWidth - 50
      })

      chart.source(this.dataChart, {
        actual: {
          max: 100,
          min: 0,
          nice: false
        }
      })

      chart.coord('polar', {
        transposed: true,
        innerRadius: 0.8,
        startAngle: -Math.PI,
        endAngle: 0
      })
      chart.axis(false)

      chart.interval()
        .position('const*expect')
        .shape('polar-tick')
        .size(10)
        .color('#F3F3F3')
        .animate(false)
      chart.interval()
        .position('const*actual')
        .shape('polar-tick')
        .size(10)
        .color('#246BFF')
        .animate({
          appear: {
            duration: 1100,
            easing: 'linear',
            animation: function animation (shape, animateCfg) {
              const startAngle = shape.attr('startAngle')
              let endAngle = shape.attr('endAngle')
              if (startAngle > endAngle) {
                endAngle += Math.PI * 2
              }
              shape.attr('endAngle', startAngle)
              shape.animate().to(Util.mix({
                attrs: {
                  endAngle
                }
              }, animateCfg)).onUpdate(function (frame) {
                const textEl = document.querySelector('#text')
                if (textEl) textEl.innerHTML = parseInt(frame * 75) + '%'
              })
            }
          }
        })
      chart.guide().html({
        position: ['50%', '80%'],
        html: `
          <div style="width: 120px;color: #246BFF;white-space: nowrap;text-align:center;">
            <p style="font-size: 23px;margin:0;">Patrick M.</p>
            <p id="text" style="font-size: 48px;margin:0;font-weight: bold;">0</p>
          </div>`
      })
      chart.render()
    }
  }
}
</script>

<style>
canvas.guage {
  border-radius: 5px;
  background-color: #1890ff;
  background-image: linear-gradient(#246BFF, #2797FF);
}
</style>
