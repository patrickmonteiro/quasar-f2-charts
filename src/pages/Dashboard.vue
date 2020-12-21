<template>
  <q-page class="container q-pa-lg">
    <div class="row q-col-gutter-sm">
      <f2-apple-watch />
      <f2-basic />
      <f2-line />
      <f2-area />
      <f2-pie />
      <f2-heatmap />
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  components: {
    F2AppleWatch: () => import('components/F2AppleWatch'),
    F2Basic: () => import('components/F2Basic'),
    F2Line: () => import('components/F2Line'),
    F2Area: () => import('components/F2Area'),
    F2Pie: () => import('components/F2Pie'),
    F2Heatmap: () => import('components/F2Heatmap')
  }
}
</script>
