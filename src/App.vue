<template>
  <div id="app">
    <address
      :initprovselectedvalue="0"
      :initcityselectedvalue="0"
      :initregionselectedvalue="0">
    </address>
  </div>
</template>

<script>
import Address from './components/Address.vue'

export default {
  components: {
    Address
  }
}
</script>
