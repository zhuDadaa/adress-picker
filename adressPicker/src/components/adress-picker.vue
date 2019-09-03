<template>
  <div id="adressPicker">
    <mt-popup v-model="showPicker" class="area-class" position="bottom" :closeOnClickModal='false'>
      <mt-picker :slots="slots" @change="onValuesChange" :show-toolbar="true">
        <div>
          <div class="edit">
            <span class="cancle" @click="cancle">取消</span>
            <span class="sure" @click="sure">确认</span>
          </div>
          <div class="title">
            <span>省</span>
            <span>市</span>
            <span>区/县</span>
            <span>乡/镇</span>
          </div>
        </div>
      </mt-picker>
    </mt-popup>
  </div>
</template>

<script>
import 'mint-ui/lib/style.css'
// 导入数据
import data from './../../static/data/data.json'
let index = 0
let index2 = 0
let index3 = 0
// 初始化省
let province = data.map(res => {
  return res.name
})
// 初始化市
let city = data[index].childs.map(res => {
  return res.name
})
// 初始化区
let area = data[index].childs[index2].childs.map(res => {
  return res.name
})
// 初始化街
let street = data[index].childs[index2].childs[index3].childs.map(res => {
  return res.name
})
export default {
  props: ['showPicker'],
  data () {
    return {
      name: '四级地址选择器',
      areaString: '',
      slots: [{
        flex: 1,
        values: province,
        className: 'slot1',
        textAlign: 'center'
      }, {
        flex: 1,
        values: city,
        className: 'slot3',
        textAlign: 'center'
      }, {
        flex: 1,
        values: area,
        className: 'slot5',
        textAlign: 'center'
      }, {
        flex: 1,
        values: street,
        className: 'slot7',
        textAlign: 'center'
      }]
    }
  },
  methods: {
    cancle () {
      this.$emit('cancle', this.showPicker)
    },
    sure () {
      this.$emit('sure', this.areaString)
    },
    onValuesChange (picker, values) {
      let one = values[0]
      let two = values[1]
      let three = values[2]
      index = province.indexOf(one)
      if (index >= 0 && province.length > 0) {
        city = data[index].childs.map(res => {
          return res.name
        })
        picker.setSlotValues(1, city)
        two = values[1]
      }

      index2 = city.indexOf(two)
      if (index2 >= 0 && city.length > 0) {
        area = data[index].childs[index2].childs.map(res => {
          return res.name
        })
        picker.setSlotValues(2, area)
        three = values[2]
      }
      index3 = area.indexOf(three)
      if (index >= 0 && index2 >= 0 && index3 >= 0) {
        street = data[index].childs[index2].childs[index3].childs.map(res => {
          return res.name
        })
        picker.setSlotValues(3, street)
        // this.slotstree[0].values = street
      }
      this.areaString = values.join(',')
    }
  }
}
</script>

<style>
  #adressPicker .picker-toolbar {
    height: 80px;
  }
  #adressPicker .picker-slot {
    font-size: .9rem;
    max-height: 60%;
  }
  #adressPicker .mint-popup-bottom {
    width: 100%;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
  }
  #adressPicker .edit {
    display: flex;
    justify-content: space-between;
    padding: 1rem;
  }
   #adressPicker .cancle {
      color: #666666;
    }
  #adressPicker  .sure {
      color: #F2402E;
    }
  #adressPicker .title {
    color: #999999;
    display: flex;
    justify-content: space-around;
  }
  #adressPicker .title  span {
      width: 25%;
      text-align: center;
    }
</style>
