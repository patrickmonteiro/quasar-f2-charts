<template>
<div class="col-md-6 col-lg-6 col-xs-12">
  <q-card>
    <q-card-section>
      <slot></slot>
    </q-card-section>
  </q-card>
</div>
</template>

<script>
export default {
  name: 'CardBase'
}
</script>
