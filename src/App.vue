<template>
  <div id="app">
    <address
      :initprovselectedvalue="19"
      :initcityselectedvalue="289"
      :initregionselectedvalue="3039"
      initaddrsindetail="新塘">
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
