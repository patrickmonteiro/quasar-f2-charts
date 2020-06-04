<template>
  <q-page class="container q-pa-sm">
    <div class="row">
      <f2-basic />
      <f2-line />
      <f2-area />
      <f2-pie />
      <f2-heatmap />
    </div>
  </q-page>
</template>

<script>
import F2Basic from 'components/F2Basic'
import F2Line from 'components/F2Line'
import F2Area from 'components/F2Area'
import F2Pie from 'components/F2Pie'
import F2Heatmap from 'components/F2Heatmap'
export default {
  name: 'PageIndex',
  components: {
    F2Basic,
    F2Line,
    F2Area,
    F2Pie,
    F2Heatmap
  }
}
</script>
