<template>
    <select v-model="selected" lazy>
        <option v-for="option in options" v-bind:value="option.value">
            {{ option.text }}
        </option>
    </select>
</template>

<script>
export default {

  name: 'Addrselect',

  props: {
    initselectedvalue: Number,
    addrs: Array
  },

  data () {
    return {
      selected: this.initselectedvalue,
      options: [{ 'text': '请选择..', 'value': '0' }].concat(this.addrs)
    }
  },

  watch: {
    addrs (val, oldVal) {
      if (val !== oldVal) {
        this.options = [{ 'text': '请选择..', 'value': '0' }].concat(val)
        this.selected = 0
      }
    }
  }

}

</script>
