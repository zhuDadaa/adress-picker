<template>
  <div class="hello">
    <h1>四级联动地址选择器</h1>
    <div class="message-item">
      <span class="title">收货地址</span>
      <input type="text" placeholder="省份 / 城市 / 区县" @click.self="showPicker = true" readonly v-model="adress">
    </div>
    <adress-picker :showPicker='showPicker' @cancle='showPicker = false' @sure='sure'></adress-picker>
  </div>
</template>

<script>
import adressPicker from './adress-picker'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      adress: '',
      showPicker: false
    }
  },
  methods: {
    sure (adress) {
      this.adress = adress
      this.showPicker = false
    }
  },
  components: {
    adressPicker
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello {
  width: 500px;
  margin: 0 auto;
}
.message-item {
border-top: 1px solid #EBEBEB;
padding: .8rem .7rem;
display: flex;
}
.title {
  color: #333333;
  font-size: .9rem;
  width: 70px;
  display: inline-block;
}
.message-item input {
  border: 0;
  outline: 0;
}
input::placeholder {
  color: #999999;
}
</style>
