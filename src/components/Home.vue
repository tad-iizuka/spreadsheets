<template>
  <v-container>
    <v-layout justify-center xs12 row class="py-1">
     <template v-for="(item, index) in headers">
        <v-flex :key="index">
          <p style="text-align: center; width: 48px;">{{ item }}</p>
        </v-flex>
      </template>
    </v-layout>
    <v-divider></v-divider>

    <template v-for="(item, index) in items">
      <v-layout justify-center xs12 :key="index" row class="py-1">
        <v-flex>
          <p style="text-align: center; width: 48px;">{{ index + 1 }}</p>
        </v-flex>
        <v-flex>
          <input type="number" v-model.number="item.carbs" @input="sumDataV(0)" style="text-align: right; width: 48px;"/>
        </v-flex>
        <v-flex>
          <input type="number" v-model.number="item.fat" @input="sumDataV(1)" style="text-align: right; width: 48px;"/>
        </v-flex>
        <v-flex>
          <input type="number" v-model.number="item.calories" @input="sumDataV(2)" style="text-align: right; width: 48px;"/>
        </v-flex>
        <v-flex>
          <input type="number" v-model.number="item.protein" @input="sumDataV(3)" style="text-align: right; width: 48px;"/>
        </v-flex>
        <v-flex>
          <input class="sum" type="number" disabled :value="sumH[index]" style="text-align: right; width: 48px;"/>
        </v-flex>
    </v-layout>
    </template>
    <v-divider></v-divider>

    <v-layout justify-center xs1 row class="py-1">
      <v-flex>
        <p style="text-align: right; width: 48px;">SUM</p>
      </v-flex>
        <template v-for="n in 4">
          <v-flex :key="n">
            <input class="sum" type="number" :value="sumV[n - 1]" disabled style="text-align: right; width: 48px;"/>
          </v-flex>
        </template>
      <v-flex>
        <input class="sum" type="number" :value="sumH[4]" disabled style="text-align: right; width: 48px;"/>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import Vue from 'vue'
export default {
  data () {
    return {
      items: [],
      sumV: [],
      sumH: [],
      headers: [
        '#',
        'carbs',
        'fat',
        'calories',
        'protein',
        'SUM'
      ],
      preset: [
        {
          value: false,
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%'
        },
        {
          value: false,
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.0,
          iron: '1%'
        },
        {
          value: false,
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%'
        },
        {
          value: false,
          name: 'Cupcake',
          calories: 305,
          fat: 3.0,
          carbs: 67,
          protein: 4.0,
          iron: '8%'
        },
        {
          value: false,
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.0,
          iron: '16%'
        },
        {
          value: false,
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: '0%'
        },
        {
          value: false,
          name: 'Lollipop',
          calories: 392,
          fat: 0.0,
          carbs: 98,
          protein: 0,
          iron: '2%'
        },
        {
          value: false,
          name: 'Honeycomb',
          calories: 408,
          fat: 3.0,
          carbs: 87,
          protein: 6.0,
          iron: '45%'
        },
        {
          value: false,
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.0,
          iron: '22%'
        },
        {
          value: false,
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: '6%'
        }
      ]
    }
  },
  created () {
    var vm = this
    this.preset.forEach(function (item) {
      vm.items.push(item)
    })
    for (var i = 0; i < 4; i++) {
      this.sumDataV(i)
    }
  },
  methods: {
    sumDataV (index) {
      var value = 0
      this.items.forEach(function (item) {
        switch (index) {
          case 0:
            value += parseInt(item.carbs)
            break
          case 1:
            value += parseInt(item.fat)
            break
          case 2:
            value += parseInt(item.calories)
            break
          case 3:
            value += parseInt(item.protein)
            break
        }
      })
      Vue.set(this.sumV, index, value)
      this.sumDataH()
    },
    sumDataH () {
      var index = 0
      var vm = this
      this.items.forEach(function (item) {
        var value = 0
        value += parseInt(item.carbs)
        value += parseInt(item.fat)
        value += parseInt(item.calories)
        value += parseInt(item.protein)
        Vue.set(vm.sumH, index, value)
        index += 1
      })
      var value = 0
      this.sumV.forEach(function (v) {
        value += v
      })
      Vue.set(vm.sumH, 4, value)
    }
  }
}
</script>

<style>
input.sum {
  /* border: solid 0.5px #eeeeee; */
  /* background-color: #eeeeee; */
  color: red;
}
</style>
