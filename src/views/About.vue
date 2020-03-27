<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div>已选择{{chooseLength}}条</div>
    <baseTable
      :tableData="tableData"
      @calcNum="calcNum"
    ></baseTable>
    <button @click="go">点击</button>
  </div>
</template>

<script>
import baseTable from './table'
export default {
  name: 'About',
  data () {
    return {
      chooseLength: 0,
      checkArr: [],
      tableData: [
        { id: 1, name: 'xxh', age: '11' },
        { id: 2, name: 'xxh', age: '12' },
        { id: 3, name: 'xxh', age: '13' },
        { id: 4, name: 'xxh', age: '14' },
        { id: 5, name: 'xxh', age: '15' }
      ],
      tableData2: [
        { id: 1, name: 'xxh', age: '11' },
        { id: 2, name: 'xxh', age: '12' },
        { id: 3, name: 'xxh', age: '13' },
        { id: 4, name: 'xxh', age: '14' },
        { id: 5, name: 'xxh', age: '15' }
      ]
    }
  },
  components: {
    baseTable
  },
  computed: {
    // checkArr () {
    //   return Array.from({ length: this.tableData.length }, () => false)
    // }
  },
  methods: {
    calcNum (data) {
      this.chooseLength = data.reduce((memo, current, index, arr) => {
        if (current) {
          memo += 1
        }
        return memo
      }, 0)
    },
    go () {
      this.tableData = this.tableData2
      console.log(this.tableData)
    }
  }
}
</script>