<template>
  <ul>
    <li class="clearfix">
      <div class="fl a">省份</div>
      <div class="fl b">
        <div class="new-select-wp" id="prov">
          <addrselect
            :initselectedvalue="initprovselectedvalue"
            :addrs="prov_addrs"
            v-model="prov_selected"
            class="select-31"
            id="prov_select"
            name="prov" lazy>
          </addrselect>
        </div>
      </div>
    </li>
    <li class="clearfix">
      <div class="fl a">市</div>
      <div class="fl b">
        <div class="new-select-wp" id="city">
          <addrselect
            :initselectedvalue="initcityselectedvalue"
            :addrs="city_addrs"
            v-model="city_selected"
            class="select-31"
            id="city_select"
            name="city" lazy>
          </addrselect>
        </div>
      </div>
    </li>
    <li class="clearfix">
      <div class="fl a">区/县</div>
      <div class="fl b">
        <div class="new-select-wp" id="region">
          <addrselect
            :initselectedvalue="initregionselectedvalue"
            :addrs="region_addrs"
            v-model="region_selected"
            class="select-31"
            id="region_select"
            name="region" lazy>
          </addrselect>
        </div>
      </div>
    </li>
    <li class="clearfix">
      <div class="fl a">具体地址</div>
      <div class="fl b">
        <textarea id="address" name="address" class="text" placeholder="请填写具体地址" required=""></textarea>
      </div>
    </li>
  </ul>
</template>
<script>
import Addrselect from './Addrselect.vue'
import addr_arr from '../CNAddr/addr_arr'

// 根据id获取市/区数据函数，动态，经常改变
function getAddrsArrayById (id) {
  return addr_arr[id].map(item => {
    return {
      'text': item[1],
      'value': item[0]
    }
  })
}

export default {

  name: 'Address',

  components: {
    Addrselect
  },

  props: {
    initprovselectedvalue: Number,
    initcityselectedvalue: Number,
    initregionselectedvalue: Number
  },

  data () {
    return {
      prov_addrs: getAddrsArrayById(0),
      city_addrs: (this.initprovselectedvalue !== '0' && this.initprovselectedvalue !== 0) ? getAddrsArrayById(this.initprovselectedvalue) : [],
      region_addrs: (this.initcityselectedvalue !== '0' && this.initcityselectedvalue !== 0) ? getAddrsArrayById(this.initcityselectedvalue) : [],
      prov_selected: this.initprovselectedvalue,
      city_selected: this.initcityselectedvalue,
      region_selected: this.initregionselectedvalue
    }
  },

  watch: {
    'prov_selected': function (val, oldVal) {
      if (val !== oldVal) {
        if (val !== '0' && val !== 0) {
          this.city_addrs = getAddrsArrayById(val)
        } else {
          this.city_addrs = []
        }
        this.city_selected = 0
      }
    },
    'city_selected': function (val, oldVal) {
      if (val !== oldVal) {
        if (val !== '0' && val !== 0) {
          console.log(val)
          this.region_addrs = getAddrsArrayById(val)
        } else {
          this.region_addrs = []
        }
        this.region_selected = 0
      }
    }
  }
}
</script>

<style>
html {
  font-size: 100%;
  height: 100%;
}

* {
  margin: 0;
  padding: 0;
  vertical-align: baseline;
  background: transparent;
  -webkit-touch-callout: none;
  -webkit-text-size-adjust: none;
  -webkit-tap-highlight-color: transparent;
  -webkit-appearance: none;
  list-style: none;
}

body,
input,
select,
textarea,
button {
  font-size: 15px;
  font-family: sans-serif;
}

body {
  min-height: 100%;
  width: 100%;
  overflow: visible;
  overflow-x: hidden;
  font-family: "微软雅黑";
  color: #3d4245;
  position: relative;
}

div {
  margin: 0 auto;
}

img {
  border: 0;
  vertical-align: middle;
}

a {
  text-decoration: none;
  color: #333333;
}

a:active {
  text-decoration: none;
  color: #a2a5aa;
}

.clearfix:after {
  content: ".";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}

*html .clearfix {
  height: 1%;
}

*+html .clearfix {
  height: 1%;
}

:focus {
  outline: none;
}

::-moz-focus-inner {
  border: 0;
}

input[type="button"],
input[type="submit"],
input[type="reset"],
input[type="disabled"] {
  -webkit-appearance: none;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none !important;
}

.fl {
  float: left;
}

.fr {
  float: right;
}

ul > li {
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
  background-color: white;
}

ul > li .a {
  width: 24.9%;
  box-sizing: border-box;
  padding-left: 10px;
  color: #333;
  line-height: 39px;
}

ul > li .b {
  width: 74.9%;
  box-sizing: border-box;
  padding-right: 10px;
}

ul > li .b > input,
ul > li .b select,
ul > li .b > textarea {
  width: 100%;
  color: #666;
  box-sizing: border-box;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-border-radius: 2px;
}

ul > li .b .select-31 {
  background-size: 15px 10px;
}
</style>
